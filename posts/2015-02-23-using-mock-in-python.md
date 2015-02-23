Testing with mock in Python:
============================

Mocking is pretty awesome in python, especially when using the [Mock](http://www.voidspace.org.uk/python/mock/) library. It simplifies making stubs when testing, covers partial mocking, setting custom return values, how they were called, etc.

However there are a few pitfalls when initially working with Mock. Some of these things are pretty obvious, but this is a quick reference for a few gotchas I found while mocking a few projects.

##### side_effect vs return_value:
You'd only use `side_effect` if you want to test something that happens in a function instead of a return value. For example if you want to test exceptions that are raised in a method, use `side_effect`:

    dork_mock = mock.Mock()
    dork_mock.some_method.side_effect = ZeroDivisionError
    dork_mock.some_method()

    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
      File "build/bdist.linux-x86_64/egg/mock.py", line 955, in __call__
      File "build/bdist.linux-x86_64/egg/mock.py", line 1010, in _mock_call
    ZeroDivisionError

##### When to use Mock vs. MagicMock

Basically with [MagicMock](http://www.voidspace.org.uk/python/mock/magicmock.html#mock.MagicMock) you can mock magic methods. That's pretty much the only difference, otherwise you should use `Mock`. as the docs say, one tiny thing to remember is that MagickMock returns set default values for some preconfigured methods:

    m = MagicMock()
    int(m) # 1

##### Patch:

Used as a context manager, it makes a specific context when your **mock**ed modules live. You'll need to use [mock.patch()](http://www.voidspace.org.uk/python/mock/patch.html) when you want to mock modules in the classes you test. e.g.:

        with mock.patch('module.to.test.first_module') as first_mock:
            with mock.patch('module.to.test.second_module') as second_mock:

If you are doing more than one, you can write is like this so your identations don't go crazy:

    with mock.patch('module.to.test.first_module') as first_mock,\
        mock.patch('module.to.test.second_module') as second_mock:

If you are mocking methods on modules, you can put them in the return value to save you some lines + style:

        with mock.patch('module.to.test.first_method', return_value='flickity flam'):

I've seen mainly the above in our test cases, but you can use `patch` as a decorator too, and mock the class as you go:

    from mock import patch
    
    @patch('class_to_mock.the_method')
    def test_the_method(self, the_method)
        the_method.return_value = 'awesome'

##### To return_value or not to return_value:

When do we use return value? It gets confusing when you are mocking methods in a chain with instantiations or mocking multiple layers of classes.

    class Phone(object):
    def __init__(self):
        self.owner = Owner()
    
    class Owner(object):
        def get_name(self):
            return 'dork'

test:

    @patch('phone.Owner')
    def test_get_owner_name(mock_owner):
            mock_owner.get_name.return_value = "awesome guy"
            phone = Phone()
            assert phone.owner.get_name() == "awesome guy" # False

The assertion returns false because `owner` is made when instantiating the `Owner` class. But we didn't actually call that instantiation. We can do that call with `return_value`:

    @patch('phone.Owner')
    def test_get_owner_name(mock_owner):
            mock_owner.return.get_name.return_value = "awesome guy"
            phone = Phone()
            assert phone.owner.get_name() == "awesome guy" # True

`nose`:
-------

#### Running a single test file:

Technically, we should be running the entire test suite to just to be sure a change didn't break another test. However, if your tests don't yet run in parallel and every 10 seconds counts... I think it wastes a lot of time as the test suite grows. So for those curious, here is how to run a single test using **nose**:

`nosetests -v -s test_name_of_file.py`

**-s** to see all your print and debug statements (doesn't gobble up stdouts), **-v** for verbose mode, showing all test run details