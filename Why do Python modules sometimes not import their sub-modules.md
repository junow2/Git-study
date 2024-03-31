In Python, modules need to be imported before they're accessible. import logging imports just the logging module. It so happens that logging is a package with submodules, but those submodules are still not automatically loaded. So, you need to explicitly import logging.handlers before you can access it.

If you're wondering why it looks like sometimes you don't need those extra imports: some packages import some or all of their submodules when they are imported -- simply by doing those imports in their __init__.py files. In other cases it might be that something else that you import, also imported logging.handlers. It doesn't matter which piece of code does the import; as long as something in your process imports logging.handlers before you access it, it'll be there. And sometimes a module that looks like a package really isn't one, like os and os.path. os isn't a package, it just imports the correct other module (for your platform) and calls it path, just so you can access it as os.path.


파이썬에서 모듈을 가져오려면 먼저 모듈을 불러와야 합니다. import logging은 로깅 모듈만 가져옵니다. 로깅은 서브모듈이 포함된 패키지이지만 이러한 서브모듈은 자동으로 로드되지 않습니다. 따라서 logging.handlers를 명시적으로 임포트해야만 액세스할 수 있습니다.

추가 import가 필요하지 않은 것처럼 보이는 이유가 궁금하다면, 일부 패키지는 import할 때 하위 모듈의 일부 또는 전부를 __init__ .py 파일에서 임포트하기만 하면 됩니다. 다른 경우에는 다른 것을 import할 때 logging.handlers도 함께 import할 수 있습니다. 어떤 코드가 import를 수행하는지는 중요하지 않습니다. 프로세스의 어떤 부분이 logging.handlers에 액세스하기 전에 import하기만 하면 됩니다. 그리고 os와 os.path처럼 패키지처럼 보이는 모듈이 실제로는 패키지가 아닌 경우도 있습니다. os는 패키지가 아니라 플랫폼에 맞는 다른 모듈을 가져와서 경로로 호출하기만 하면 os.path로 액세스할 수 있습니다.

https://stackoverflow.com/questions/3781522/why-do-python-modules-sometimes-not-import-their-sub-modules