---
layout: post
title: 使用mock进行单元测试(python)
date: 2016-09-21
tags:
- python
---

此代码涵盖了mock的基本用法，代码来源于mock文档 [mock doc](http://www.voidspace.org.uk/python/mock/getting-started.html)


``` python

from mock import MagicMock, Mock, patch, ANY
# 1.使用mock 替换对象中的方法
# mock.assert_called_once_with 用于验证调用参数是否正确

class ProductionClass(object):
    def method(self):
        self.something(1, 2, 3)
    def something(self, a, b, c):
        pass

real = ProductionClass()
real.something = MagicMock()
real.method()
real.something.assert_called_once_with(1, 2, 3)


# 2.使用mock 替代传入参数
# assert_called_with 用于验证依赖对像是否被正确使用

class ProductionClass(object):
    def closer(self, something):
        something.close()

real = ProductionClass()
mock = Mock()
real.closer(mock)
mock.close.assert_called_with()


# 3.使用Mock 替换Class
# 替换类于替换方法类似

# 例子需要构造module模块
import sys
sys.modules['module'] = Mock()
import module

def calculate():
    instance = module.Helper()
    return instance.getFactor() *3

with patch('module.Helper') as mock:
    instance = mock.return_value
    instance.getFactor.return_value = 1
    result = calculate()
    instance.getFactor.assert_called_once_with() #方法被正确调用
    assert result == 3 #验证结果是否正确

# 4. side_effect, literate

mock = MagicMock(side_effect=[4, 5, 6])
assert mock()==4
assert mock()==5
assert mock()==6

# 5. side_effect, Exception
mock = Mock(side_effect=Exception('Boom!'))

# 6. side_effect, function
vals = {(1, 2): 1, (2, 3): 2}
def side_effect(*args):
    return vals[args]

mock = MagicMock(side_effect=side_effect)
assert 1==mock(1, 2)
assert 2==mock(2, 3)

# 7. 基于类/对象为模板创建对象
# 使用模版不存在的方法或者属性会报错
class SomeClass(object):
    pass

a = SomeClass()
mock = Mock(spec=a)
#mock.a
#mock.old_method() # 报错

# 8. mock 调用多次
returns = [1, 2]

def side_effect(*args):
  result = returns.pop(0)
  if isinstance(result, Exception):
    raise result
  return result

mock = Mock(side_effect=side_effect)
assert 1==mock('first')
assert 2==mock('second')

# 9. patch应用到多个
from unittest2 import TestCase
@patch('module.SomeClass')
class MyTest(TestCase):

    def test_one(self, MockSomeClass):
        self.assertTrue(module.SomeClass is MockSomeClass)

    def test_two(self, MockSomeClass):
        self.assertTrue(module.SomeClass is MockSomeClass)

    def not_a_test(self):
        return 'something'

MyTest('test_one').test_one()
MyTest('test_two').test_two()
MyTest('test_two').not_a_test()

class MyTest(TestCase):
    def setUp(self):
        self.patcher = patch('module.foo')
        self.mock_foo = self.patcher.start()

    def test_foo(self):
        self.assertTrue(module.foo is self.mock_foo)

    def tearDown(self):
        self.patcher.stop()

MyTest('test_foo').run()

# 10. ANY
mock = Mock(return_value=None)
mock('foo', bar=object())
mock.assert_called_once_with('foo', bar=ANY)


```
