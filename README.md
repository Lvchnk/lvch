# lvch
#1 
def fact(x):
    if x == 1 or x == 0:
        return 1
    else:
        return fact(x - 1) * x


#2
def filter_even(li):
    return list(filter(lambda x: x % 2 == 0, li))


#3
def square(li):
    return list(map(lambda x: x ** 2, li))


#4
def bin_search(li, element):
    l = 0
    r = len(li) - 1
    while r >= l:
        mid = (r + l) // 2
        if li[mid] > element:
            r = mid - 1
        elif li[mid] < element:
            l = mid + 1
        else:
            return mid
    return -1


#5
def is_palindrome(string):
    string = ''.join(filter(lambda x: x.isalpha(), string))
    start = 0
    finish = len(string) - 1
    while start != len(string) // 2:
        if string[start].lower() != string[finish].lower():
            return "NO"
        start += 1
        finish -= 1
    return "YES"


#6
OPS = {'+': lambda x, y: x + y, '-': lambda x, y: x - y,
       '*': lambda x, y: x * y, '//': lambda x, y: x // y,
       '%': lambda x, y: x % y, '**': lambda x, y: x ** y}


def load_file(filename):
    file = open(filename, encoding='utf-8')
    data = [line.strip().split('    ') for line in file.readlines()]
    file.close()
    return data


def evaluate(l_number, r_number, op):
    if op in OPS:
        return OPS[op](l_number, r_number)
    else:
        print('Неизвестная операция')


def calculate(path2file):
    data = load_file(path2file)
    operation = 0
    f_operand = 1
    s_operand = 2
    result = []
    for exp in data:
        result.append(str(evaluate(int(exp[f_operand]), int(exp[s_operand]), exp[operation])))
    return ','.join(result)


#7
def load_file2(filename):
    file = open(filename, encoding='utf-8')
    data = [line for line in file.readlines()]
    file.close()
    return data


def substring_slice(path2file_1, path2file_2):
    data_1 = load_file2(path2file_1)
    data_2 = load_file2(path2file_2)
    result = []
    for line_1, line_2 in zip(data_1, data_2):
        start_index, end_index = map(int, line_2.strip().split())
        result.append(line_1[start_index:end_index + 1])
    return ' '.join(result)


#8
import json


def decode_ch(string_of_elements):
    periodic_table = json.load(open('periodic_table.json', encoding='utf-8'))
    search_index = 1
    result = ''
    while string_of_elements:
        last_ch = string_of_elements[search_index:search_index + 1].isupper() \
            if string_of_elements[search_index:search_index + 1] else True
        if string_of_elements[:search_index] in periodic_table and last_ch:
            result += periodic_table[string_of_elements[:search_index]]
            string_of_elements = string_of_elements[search_index:]
            search_index = 1
        else:
            search_index += 1
    return result


#9
class Student:
    def __init__(self, name, surname, grades=None):
        self.name = name
        self.surname = surname
        self.fullname = name + ' ' + surname
        if grades is None:
            grades = [3, 4, 5]
        self.grades = grades

    def is_otlichnik(self):
        return 'Yes' if self.mean_grade() >= 4.5 else 'NO'

    def greeting(self):
        return f'Hello, I am {self.fullname}'

    def mean_grade(self):
        return sum(self.grades) / len(self.grades)

    def __add__(self, other):
        return f'{self.name} is friends with {other.name}'

    def __str__(self):
        return self.fullname


#10
class MyError(Exception):
    def __init__(self, msg):
        self.msg = msg
        super().__init__(msg)
