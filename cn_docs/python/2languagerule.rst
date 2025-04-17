:tocdepth: 2

:orphan:

.. _s2-python-language-rules:
.. _2-python-language-rules:

.. _python-language-rules:

2 Python 语言规则
=================================

2 Python Language Rules 

.. _s2.1-lint:
.. _21-lint:

.. _lint:


2.1 Lint
--------------

2.1 Lint 

.. tab:: 中文

    使用此 `pylintrc <https://google.github.io/styleguide/pylintrc>`_ 在您的代码上运行 `pylint`。

.. tab:: 英文

    Run `pylint` over your code using this `pylintrc <https://google.github.io/styleguide/pylintrc>`_ .

.. _s2.1.1-definition:
.. _211-definition:

.. _lint-definition:


2.1.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.1.1 Definition 

.. tab:: 中文

    `pylint` 是一款用于查找 Python 源代码中的错误和代码风格问题的工具。它可以发现一些通常被 C 和 C++ 等动态性较差的语言的编译器捕获的问题。由于 Python 的动态特性，某些警告可能不正确；但是，虚假警告应该很少出现。

.. tab:: 英文

    `pylint` is a tool for finding bugs and style problems in Python source code. It finds problems that are typically caught by a compiler for less dynamic languages like C and C++. Because of the dynamic nature of Python, some warnings may be incorrect; however, spurious warnings should be fairly infrequent.

.. _s2.1.2-pros:
.. _212-pros:

.. _lint-pros:


2.1.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.1.2 Pros 

.. tab:: 中文

    捕捉容易错过的错误，如拼写错误、赋值前使用变量等。

.. tab:: 英文

    Catches easy-to-miss errors like typos, using-vars-before-assignment, etc.

.. _s2.1.3-cons:
.. _213-cons:

.. _lint-cons:


2.1.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.1.3 Cons 

.. tab:: 中文

    `pylint` 并不完美。为了充分利用它，有时我们需要绕过它，抑制它的警告，或者修复它。

.. tab:: 英文

    `pylint` isn't perfect. To take advantage of it, sometimes we'll need to write around it, suppress its warnings or fix it.

.. _s2.1.4-decision:
.. _214-decision:

.. _lint-decision:


2.1.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.1.4 Decision 

.. tab:: 中文

    确保对你的代码运行 `pylint`。

    如果某些警告不适用，应将其抑制，以避免掩盖其他问题。要抑制警告，可以添加一行级注释：

    .. code-block:: python

        def do_PUT(self):  # WSGI 名称，因此 pylint: disable=invalid-name
        ...

    每个 :code:`pylint` 警告都有一个符号名称（如 :code:`empty-docstring`），Google 特定的警告则以 :code:`g-` 开头。

    如果从符号名称无法清晰看出抑制原因，应添加说明。

    以这种方式抑制的好处是，我们可以轻松搜索出这些抑制点并重新评估。

    你可以通过以下命令获取所有 :code:`pylint` 警告列表：

    .. code-block:: shell

        pylint --list-msgs

    如需获取某个特定警告的详细信息，可使用：

    .. code-block:: shell

        pylint --help-msg=invalid-name

    优先使用 :code:`pylint: disable`，而非已弃用的旧格式 :code:`pylint: disable-msg`。

    对于未使用的参数警告，可以在函数开始处删除该变量来抑制。务必附带注释说明为何删除，使用 “Unused.” 即可。例如：

    .. code-block:: python

        def viking_cafe_order(spam: str, beans: str, eggs: str | None = None) -> str:
            del beans, eggs  # Unused by vikings.
            return spam + spam + spam

    其他常见的抑制方式包括使用 ':code:`_`' 作为未使用参数的标识符，或为参数名前加上 ':code:`unused_`' 前缀，或者将它们赋值给 '`_`'。这些方式是允许的，但已不再推荐。它们会破坏基于命名参数调用的代码，并且无法强制确保参数确实未被使用。

.. tab:: 英文

    Make sure you run :code:`pylint` on your code.


    Suppress warnings if they are inappropriate so that other issues are not hidden. To suppress warnings, you can set a line-level comment:

    .. code-block:: python

        def do_PUT(self):  # WSGI name, so pylint: disable=invalid-name
        ...


    :code:`pylint` warnings are each identified by symbolic name (:code:`empty-docstring`) Google-specific warnings start with :code:`g-`.

    If the reason for the suppression is not clear from the symbolic name, add an explanation.

    Suppressing in this way has the advantage that we can easily search for suppressions and revisit them.

    You can get a list of :code:`pylint` warnings by doing:

    .. code-block:: shell

        pylint --list-msgs


    To get more information on a particular message, use:

    .. code-block:: shell
        
        pylint --help-msg=invalid-name


    Prefer :code:`pylint: disable` to the deprecated older form :code:`pylint: disable-msg`.

    Unused argument warnings can be suppressed by deleting the variables at the
    beginning of the function. Always include a comment explaining why you are
    deleting it. "Unused." is sufficient. For example:

    .. code-block:: python

        def viking_cafe_order(spam: str, beans: str, eggs: str | None = None) -> str:
            del beans, eggs  # Unused by vikings.
            return spam + spam + spam

    Other common forms of suppressing this warning include using ':code:`_`' as the
    identifier for the unused argument or prefixing the argument name with
    ':code:`unused_`', or assigning them to '`_`'. These forms are allowed but no longer
    encouraged. These break callers that pass arguments by name and do not enforce
    that the arguments are actually unused.

.. _s2.2-imports:
.. _22-imports:

.. _imports:

2.2 导入
--------------

2.2 Imports 

.. tab:: 中文

    仅对包和模块使用 :code:`import` 语句，而不是对单个类型、类或函数使用。

.. tab:: 英文

    Use :code:`import` statements for packages and modules only, not for individual types, classes, or functions.

.. _s2.2.1-definition:
.. _221-definition:

.. _imports-definition:

2.2.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.2.1 Definition 

.. tab:: 中文

    从一个模块到另一个模块共享代码的可重用机制。

.. tab:: 英文

    Reusability mechanism for sharing code from one module to another.

.. _s2.2.2-pros:
.. _222-pros:

.. _imports-pros:

2.2.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.2.2 Pros 

.. tab:: 中文

    命名空间管理约定很简单。每个标识符的来源都以一致的方式指示； ``x.Obj`` 表示对象 ``Obj`` 在模块 ``x`` 中定义。

.. tab:: 英文

    The namespace management convention is simple. The source of each identifier is indicated in a consistent way; :code:`x.Obj` says that object :code:`Obj` is defined in module `x`.

.. _s2.2.3-cons:
.. _223-cons:

.. _imports-cons:

2.2.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.2.3 Cons 

.. tab:: 中文

    模块名称仍然可能冲突。有些模块名称太长，不方便使用。

.. tab:: 英文

    Module names can still collide. Some module names are inconveniently long.

.. _s2.2.4-decision:
.. _224-decision:

.. _imports-decision:

2.2.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.2.4 Decision 

.. tab:: 中文

    * 导入包和模块时使用 :code:`import x`。
    * 当 :code:`x` 是包前缀而 :code:`y` 是不带前缀的模块名时，使用 :code:`from x import y`。
    * 在以下任一情形中使用 :code:`from x import y as z`：

      - 需要导入两个名称为 :code:`y` 的模块。
      - :code:`y` 与当前模块中定义的顶层名称冲突。
      - :code:`y` 与公共 API 中常见的参数名称冲突（例如 :code:`features`）。
      - :code:`y` 名称过长，不便使用。
      - :code:`y` 在当前代码上下文中名称过于通用（例如：:code:`from storage.file_system import options as fs_options` ）。

    * 仅当 :code:`z` 是标准缩写时，才使用 :code:`import y as z`（例如：`import numpy as np`）。

    例如，可以如下方式导入模块 :code:`sound.effects.echo`：

    .. code-block:: python

        from sound.effects import echo
        ...
        echo.EchoFilter(input, output, delay=0.7, atten=4)

    不要在导入中使用相对路径名称。即使模块位于同一包中，也应使用完整的包名称。这有助于避免无意中重复导入某个包。

.. tab:: 英文

    * Use :code:`import x` for importing packages and modules.
    * Use :code:`from x import y` where :code:`x` is the package prefix and :code:`y` is the module name with no prefix.
    * Use :code:`from x import y as z` in any of the following circumstances:
      - Two modules named :code:`y` are to be imported.
      - :code:`y` conflicts with a top-level name defined in the current module.
      - :code:`y` conflicts with a common parameter name that is part of the public API (e.g., :code:`features`).
      - :code:`y` is an inconveniently long name.
      - :code:`y` is too generic in the context of your code (e.g., :code:`from storage.file_system import options as fs_options`).
    * Use :code:`import y as z` only when `z` is a standard abbreviation (e.g., :code:`import numpy as np`).
    
    For example the module :code:`sound.effects.echo` may be imported as follows:
    
    .. code-block:: python
    
        from sound.effects import echo
        ...
        echo.EchoFilter(input, output, delay=0.7, atten=4)
    
    Do not use relative names in imports. Even if the module is in the same package,
    use the full package name. This helps prevent unintentionally importing a
    package twice.

.. _imports-exemptions:


2.2.4.1 豁免
""""""""""""""""""""""""""""""""""""

2.2.4.1 Exemptions 

.. tab:: 中文

    以下情形可不遵守此规则：

    * 来自以下模块的符号用于支持静态分析和类型检查：

      - :code:`typing` 模块 - 见 :ref:`typing-imports`
      - :code:`collections.abc` 模块 - 见 :ref:`typing-imports`
      - `typing_extensions <https://github.com/python/typing_extensions/blob/main/README.md>`_ 模块

    * 来自 `six.moves module <https://six.readthedocs.io/#module-six.moves>`_ 的重定向导入。

.. tab:: 英文

    Exemptions from this rule:

    * Symbols from the following modules are used to support static analysis and type checking:
    
      * :code:`typing` module - see :ref:`typing-imports`
      * :code:`collections.abc` module - see :ref:`typing-imports`
      * `typing_extensions <https://github.com/python/typing_extensions/blob/main/README.md>`_ module
    
    * Redirects from the `six.moves <https://six.readthedocs.io/#module-six.moves>`_ module

.. _s2.3-packages:
.. _23-packages:

.. _packages:

2.3 包
----------------------------

2.3 Packages 

.. tab:: 中文

    使用模块的完整路径名位置导入每个模块。

.. tab:: 英文

    Import each module using the full pathname location of the module.

.. _s2.3.1-pros:
.. _231-pros:

.. _packages-pros:

2.3.1 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.3.1 Pros 

.. tab:: 中文

    避免由于模块搜索路径不符合作者预期而导致模块名称冲突或导入错误。使模块查找更加便捷。

.. tab:: 英文

    Avoids conflicts in module names or incorrect imports due to the module search path not being what the author expected. Makes it easier to find modules.

.. _s2.3.2-cons:
.. _232-cons:

.. _packages-cons:

2.3.2 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.3.2 Cons 

.. tab:: 中文

    由于必须复制包的层次结构，代码部署会变得更加困难。对于现代部署机制来说，这并非什么问题。

.. tab:: 英文

    Makes it harder to deploy code because you have to replicate the package hierarchy. Not really a problem with modern deployment mechanisms.

.. _s2.3.3-decision:
.. _233-decision:

.. _packages-decision:

2.3.3 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.3.3 Decision 

.. tab:: 中文

    所有新代码都应通过完整的包名称导入模块。

    导入语句应如下所示：

    .. code-block:: python

        Yes:
        # 在代码中通过完整名称引用 absl.flags（较为冗长但清晰）。
        import absl.flags
        from doctor.who import jodie

        _FOO = absl.flags.DEFINE_string(...)

    .. code-block:: python

        Yes:
        # 在代码中仅通过模块名引用 flags（常见做法）。
        from absl import flags
        from doctor.who import jodie

        _FOO = flags.DEFINE_string(...)

    *(假设该文件位于* ``doctor/who/`` ，*且* ``jodie.py`` *也在同一目录中)*

    .. code-block:: python

        No:
        # 无法明确作者希望导入哪个模块，也无法确定实际会导入哪个模块。
        # 实际的导入行为依赖于控制 sys.path 的外部因素。
        # 作者是想导入哪个 jodie 模块？
        import jodie

    不应假设主程序所在目录会自动添加到 :code:`sys.path` 中，尽管在某些环境中确实如此。  
    因此，代码应默认 :code:`import jodie` 指的是某个第三方或顶层包 :code:`jodie`，而非本地的 :code:`jodie.py` 文件。

.. tab:: 英文

    All new code should import each module by its full package name.

    Imports should be as follows:

    .. code-block:: python

        Yes:
        # Reference absl.flags in code with the complete name (verbose).
        import absl.flags
        from doctor.who import jodie

        _FOO = absl.flags.DEFINE_string(...)

    .. code-block:: python
        
        Yes:
        # Reference flags in code with just the module name (common).
        from absl import flags
        from doctor.who import jodie

        _FOO = flags.DEFINE_string(...)

    *(assume this file lives in* :code:`doctor/who/` *where* :code:`jodie.py` *also exists)*

    .. code-block:: python
        
        No:
        # Unclear what module the author wanted and what will be imported.  The actual
        # import behavior depends on external factors controlling sys.path.
        # Which possible jodie module did the author intend to import?
        import jodie

    The directory the main binary is located in should not be assumed to be in
    :code:`sys.path` despite that happening in some environments. This being the case,
    code should assume that :code:`import jodie` refers to a third-party or top-level
    package named :code:`jodie`, not a local :code:`jodie.py`.


.. _s2.4-exceptions:
.. _24-exceptions:

.. _exceptions:

2.4 异常
----------------------------

2.4 Exceptions 

.. tab:: 中文

    允许例外，但必须谨慎使用。

.. tab:: 英文

    Exceptions are allowed but must be used carefully.

.. _s2.4.1-definition:
.. _241-definition:

.. _exceptions-definition:

2.4.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.4.1 Definition 

.. tab:: 中文

    异常是打破正常控制流来处理错误或其他异常情况的一种手段。

.. tab:: 英文

    Exceptions are a means of breaking out of normal control flow to handle errors or other exceptional conditions.

.. _s2.4.2-pros:
.. _242-pros:

.. _exceptions-pros:

2.4.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.4.2 Pros 

.. tab:: 中文

    正常操作代码的控制流不会被错误处理代码弄得杂乱无章。它还允许控制流在特定条件发生时跳过多个帧，例如，一步即可从 N 个嵌套函数返回，而无需逐一查找错误代码。

.. tab:: 英文

    The control flow of normal operation code is not cluttered by error-handling
    code. It also allows the control flow to skip multiple frames when a certain
    condition occurs, e.g., returning from N nested functions in one step instead of
    having to plumb error codes through.

.. _s2.4.3-cons:
.. _243-cons:

.. _exceptions-cons:

2.4.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.4.3 Cons 

.. tab:: 中文

    可能导致控制流混乱。调用库时容易遗漏错误情况。

.. tab:: 英文

    May cause the control flow to be confusing. Easy to miss error cases when making library calls.

.. _s2.4.4-decision:
.. _244-decision:

.. _exceptions-decision:

2.4.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.4.4 Decision 

.. tab:: 中文

    异常的使用必须遵循以下要求：
    
    - 在合适的情况下使用内建异常类。例如，当违反前置条件（如函数参数校验）时，抛出 :code:`ValueError` 以表示程序设计错误。
    
    - 不应使用 :code:`assert` 语句替代条件语句或前置条件验证。 :code:`assert` 语句不能作为应用逻辑的关键部分。判断依据是：移除该 :code:`assert` 后，代码仍应能正常运行。 :code:`assert` 条件并不保证一定会被执行，详见  
      `官方文档说明 <https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement>`_。  
      在使用 `pytest <https://pytest.org>`_ 进行测试时，可以且应该使用 :code:`assert` 来验证预期行为。例如：
      
      .. code-block:: python
  
          Yes:
          def connect_to_next_port(self, minimum: int) -> int:
              """连接到下一个可用端口。
  
              参数：
              minimum：大于或等于 1024 的端口号。
  
              返回：
              新的最小端口值。
  
              异常：
              ConnectionError：如果找不到可用端口。
              """
              if minimum < 1024:
                  # 注意，这里的 ValueError 没有出现在文档字符串的 "Raises:" 部分，
                  # 因为不应对 API 误用行为的特定反应提供保证。
                  raise ValueError(f'Min. port must be at least 1024, not {minimum}.')
              port = self._find_next_open_port(minimum)
              if port is None:
                  raise ConnectionError(
                      f'Could not connect to service on port {minimum} or higher.')
              # 程序逻辑并不依赖于这个 assert 的结果。
              assert port >= minimum, (
                  f'Unexpected port {port} when minimum was {minimum}.')
              return port
  
      .. code-block:: python
  
          No:
          def connect_to_next_port(self, minimum: int) -> int:
              """连接到下一个可用端口。
  
              参数：
              minimum：大于或等于 1024 的端口号。
  
              返回：
              新的最小端口值。
              """
              assert minimum >= 1024, 'Minimum port must be at least 1024.'
              # 后续代码依赖于上述 assert。
              port = self._find_next_open_port(minimum)
              assert port is not None
              # 返回语句的类型检查依赖于该 assert。
              return port
    
    - 库或包可以定义自定义异常，但必须继承自某个已有的异常类。异常名称应以 :code:`Error` 结尾，且不应出现重复命名（如 :code:`foo.FooError`）。
    
    - 不要使用捕获所有异常的 :code:`except:` 语句，也不要捕获 :code:`Exception` 或 :code:`StandardError`，除非你：
    
      - 要重新抛出该异常，或  
      - 要创建程序中的一个“隔离点”，在该位置异常不会被继续传播，而是被记录或忽略，例如为了防止线程崩溃而保护其最外层的代码块。
    
      Python 在这方面非常宽容， :code:`except:` 会捕获所有内容，包括拼写错误的名称、`sys.exit()` 调用、按下 Ctrl+C、单元测试失败等各种你并不想捕获的异常。
    
    - 尽量减少 :code:`try`/:code:`except` 块中包含的代码量。:code:`try` 块越大，越有可能捕获到你意料之外的异常。在这种情况下，:code:`try`/:code:`except` 可能会掩盖真正的错误。
    
    - 使用 :code:`finally` 子句来编写无论是否发生异常都需要执行的代码。这在进行清理操作时非常有用，比如关闭文件。

.. tab:: 英文

    Exceptions must follow certain conditions:
    
    - Make use of built-in exception classes when it makes sense. For example,
      raise a :code:`ValueError` to indicate a programming mistake like a violated
      precondition, such as may happen when validating function arguments.
    
    - Do not use :code:`assert` statements in place of conditionals or validating
      preconditions. They must not be critical to the application logic. A litmus
      test would be that the :code:`assert` could be removed without breaking the code.
      :code:`assert` conditionals are
      not guaranteed `<https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement>`_ 
      to be evaluated. For `pytest <https://pytest.org>`_  based tests, :code:`assert` is
      okay and expected to verify expectations. For
      example:
    
        
      .. code-block:: python

        Yes:
        def connect_to_next_port(self, minimum: int) -> int:
            """Connects to the next available port.

            Args:
            minimum: A port value greater or equal to 1024.

            Returns:
            The new minimum port.

            Raises:
            ConnectionError: If no available port is found.
            """
            if minimum < 1024:
            # Note that this raising of ValueError is not mentioned in the doc
            # string's "Raises:" section because it is not appropriate to
            # guarantee this specific behavioral reaction to API misuse.
              raise ValueError(f'Min. port must be at least 1024, not {minimum}.')
              port = self._find_next_open_port(minimum)
              if port is None:
              raise ConnectionError(
                  f'Could not connect to service on port {minimum} or higher.')
              # The code does not depend on the result of this assert.
              assert port >= minimum, (
                  f'Unexpected port {port} when minimum was {minimum}.')
              return port
    
      .. code-block:: python
  
          No:
          def connect_to_next_port(self, minimum: int) -> int:
              """Connects to the next available port.
  
              Args:
              minimum: A port value greater or equal to 1024.
  
              Returns:
              The new minimum port.
              """
              assert minimum >= 1024, 'Minimum port must be at least 1024.'
              # The following code depends on the previous assert.
              port = self._find_next_open_port(minimum)
              assert port is not None
              # The type checking of the return statement relies on the assert.
              return port
    
    
    - Libraries or packages may define their own exceptions. When doing so they
      must inherit from an existing exception class. Exception names should end in
      :code:`Error` and should not introduce repetition (:code:`foo.FooError`).
    
    - Never use catch-all :code:`except:` statements, or catch :code:`Exception` or
      :code:`StandardError`, unless you are
    
      - re-raising the exception, or
      - creating an isolation point in the program where exceptions are not
        propagated but are recorded and suppressed instead, such as protecting a
        thread from crashing by guarding its outermost block.
    
      Python is very tolerant in this regard and :code:`except:` will really catch
      everything including misspelled names, sys.exit() calls, Ctrl+C interrupts,
      unittest failures and all kinds of other exceptions that you simply don't
      want to catch.
    
    - Minimize the amount of code in a :code:`try`/:code:`except` block. The larger the body
      of the :code:`try`, the more likely that an exception will be raised by a line of
      code that you didn't expect to raise an exception. In those cases, the
      :code:`try`/:code:`except` block hides a real error.
    
    - Use the :code:`finally` clause to execute code whether or not an exception is
      raised in the :code:`try` block. This is often useful for cleanup, i.e., closing a
      file.

.. _s2.5-global-variables:
.. _25-global-variables:
.. _s2.5-global-state:
.. _25-global-state:

.. _global-variables:

2.5 可变全局状态
----------------------------

2.5 Mutable Global State 

.. tab:: 中文

    避免可变的全局状态。

.. tab:: 英文

    Avoid mutable global state.

.. _s2.5.1-definition:
.. _251-definition:

.. _global-variables-definition:

2.5.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.5.1 Definition 

.. tab:: 中文

    程序执行期间可能发生变异的模块级值或类属性。

.. tab:: 英文

    Module-level values or class attributes that can get mutated during program execution.

.. _s2.5.2-pros:
.. _252-pros:

.. _global-variables-pros:

2.5.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.5.2 Pros 

.. tab:: 中文

    偶尔有用。

.. tab:: 英文

    Occasionally useful.

.. _s2.5.3-cons:
.. _253-cons:

.. _global-variables-cons:

2.5.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.5.3 Cons 

.. tab:: 中文

    * 打破封装性：这类设计可能会妨碍实现合理的目标。例如，如果使用全局状态来管理数据库连接，那么同时连接两个不同的数据库（例如在迁移期间用于比较差异）将变得困难。类似的问题也很容易出现在全局注册表的使用中。

    * 有可能在模块导入期间改变模块的行为，因为全局变量的赋值是在模块首次导入时执行的。

.. tab:: 英文

    * Breaks encapsulation: Such design can make it hard to achieve valid objectives. For example, if global state is used to manage a database connection, then connecting to two different databases at the same time (such as for computing differences during a migration) becomes difficult. Similar problems easily arise with global registries.

    * Has the potential to change module behavior during the import, because assignments to global variables are done when the module is first imported.

.. _s2.5.4-decision:
.. _254-decision:

.. _global-variables-decision:

2.5.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.5.4 Decision 

.. tab:: 中文

    避免使用可变的全局状态。

    在极少数确有必要使用全局状态的情况下，应将可变的全局实体声明在模块级别或作为类属性，并通过在名称前加下划线 `_` 使其成为内部实现。如有必要，外部对可变全局状态的访问必须通过公共函数或类方法进行。参见下文的 :ref:`命名规范 <s3.16-naming>`。请在注释中或注释中链接的文档中说明使用可变全局状态的设计原因。

    允许并鼓励使用模块级常量。例如：用于内部用途的常量 `_MAX_HOLY_HANDGRENADE_COUNT = 3`，或用于公共 API 的常量 `SIR_LANCELOTS_FAVORITE_COLOR = "blue"`。常量名称必须使用全大写加下划线的格式。参见下文的 :ref:`命名规范 <s3.16-naming>` 。


.. tab:: 英文

    Avoid mutable global state.

    In those rare cases where using global state is warranted, mutable global
    entities should be declared at the module level or as a class attribute and made
    internal by prepending an `_` to the name. If necessary, external access to
    mutable global state must be done through public functions or class methods. See
    :ref:`Naming <s3.16-naming>` below. Please explain the design reasons why mutable
    global state is being used in a comment or a doc linked to from a comment.

    Module-level constants are permitted and encouraged. For example:
    `_MAX_HOLY_HANDGRENADE_COUNT = 3` for an internal use constant or
    `SIR_LANCELOTS_FAVORITE_COLOR = "blue"` for a public API constant. Constants
    must be named using all caps with underscores. See :ref:`Naming <s3.16-naming>`
    below.

.. _s2.6-nested:
.. _26-nested:

.. _nested-classes-functions:

2.6 嵌套/本地/内部类和函数
----------------------------

2.6 Nested/Local/Inner Classes and Functions 

.. tab:: 中文

    嵌套的局部函数或类可以用来覆盖局部变量。内部类也很好。

.. tab:: 英文

    Nested local functions or classes are fine when used to close over a local variable. Inner classes are fine.

.. _s2.6.1-definition:
.. _261-definition:

.. _nested-classes-functions-definition:

2.6.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.6.1 Definition 

.. tab:: 中文

    类可以在方法、函数或类内部定义。函数可以在方法或函数内部定义。嵌套函数对封闭作用域中定义的变量具有只读访问权限。

.. tab:: 英文

    A class can be defined inside of a method, function, or class. A function can be defined inside a method or function. Nested functions have read-only access to variables defined in enclosing scopes.

.. _s2.6.2-pros:
.. _262-pros:

.. _nested-classes-functions-pros:

2.6.2优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.6.2 Pros 

.. tab:: 中文

    允许定义仅在非常有限的范围内使用的实用程序类和函数。非常符合 `ADT <https://en.wikipedia.org/wiki/Abstract_data_type>`_ 规范。常用于实现装饰器。

.. tab:: 英文

    Allows definition of utility classes and functions that are only used inside of a very limited scope. Very `ADT <https://en.wikipedia.org/wiki/Abstract_data_type>`_ -y. Commonly used for implementing decorators.

.. _s2.6.3-cons:
.. _263-cons:

.. _nested-classes-functions-cons:

2.6.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.6.3 Cons 

.. tab:: 中文

    嵌套函数和类无法直接测试。嵌套会使外部函数变得更长，可读性更差。

.. tab:: 英文

    Nested functions and classes cannot be directly tested. Nesting can make the outer function longer and less readable.

.. _s2.6.4-decision:
.. _264-decision:

.. _nested-classes-functions-decision:

2.6.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.6.4 Decision 

.. tab:: 中文

    它们没有问题，但有一些注意事项。避免使用嵌套函数或类，除非需要覆盖除 :code:`self` 或 :code:`cls` 之外的本地值。不要仅仅为了向模块用户隐藏函数而嵌套函数。相反，应该在模块级别为其名称添加 ``_`` 前缀，以便测试仍然可以访问它。

.. tab:: 英文

    They are fine with some caveats. Avoid nested functions or classes except when closing over a local value other than :code:`self` or :code:`cls`. Do not nest a function just to hide it from users of a module. Instead, prefix its name with an ``_`` at the module level so that it can still be accessed by tests.

.. _s2.7-comprehensions:
.. _s2.7-list_comprehensions:
.. _27-list_comprehensions:
.. _list_comprehensions:
.. _list-comprehensions:

.. _comprehensions:

2.7 推导式与生成器表达式
----------------------------

2.7 Comprehensions & Generator Expressions 

.. tab:: 中文

    可以用于简单的情况。

.. tab:: 英文

    Okay to use for simple cases.

.. _s2.7.1-definition:
.. _271-definition:

.. _comprehensions-definition:

2.7.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.7.1 Definition 

.. tab:: 中文

    列表、字典和集合推导以及生成器表达式提供了一种简洁有效的方法来创建容器类型和迭代器，而无需使用传统循环、:code:`map()`、:code:`filter()` 或 :code:`lambda`。

.. tab:: 英文

    List, Dict, and Set comprehensions as well as generator expressions provide a concise and efficient way to create container types and iterators without resorting to the use of traditional loops, :code:`map()`, :code:`filter()`, or :code:`lambda`.

.. _s2.7.2-pros:
.. _272-pros:

.. _comprehensions-pros:

2.7.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.7.2 Pros 

.. tab:: 中文

    简单的推导式比其他字典、列表或集合的创建技术更清晰、更简洁。生成器表达式可以非常高效，因为它们完全避免了创建列表。

.. tab:: 英文

    Simple comprehensions can be clearer and simpler than other dict, list, or set creation techniques. Generator expressions can be very efficient, since they avoid the creation of a list entirely.

.. _s2.7.3-cons:
.. _273-cons:

.. _comprehensions-cons:

2.7.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.7.3 Cons 

.. tab:: 中文

    复杂的理解或生成器表达式可能难以阅读。

.. tab:: 英文

    Complicated comprehensions or generator expressions can be hard to read.

.. _s2.7.4-decision:
.. _274-decision:

.. _comprehensions-decision:

2.7.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.7.4 Decision 

.. tab:: 中文

    允许使用推导式，但不允许使用多个 :code:`for` 子句或过滤表达式。优化重点在于可读性，而非简洁性。

.. tab:: 英文

    Comprehensions are allowed, however multiple :code:`for` clauses or filter expressions are not permitted. Optimize for readability, not conciseness.

.. code-block:: python

    Yes:
        result = [mapping_expr for value in iterable if filter_expr]

        result = [
            is_valid(metric={'key': value})
            for value in interesting_iterable
                if a_longer_filter_expression(value)
        ]

        descriptive_name = [
            transform({'key': key, 'value': value}, color='black')
            for key, value in generate_iterable(some_input)
                if complicated_condition_is_met(key, value)
        ]

        result = []
        for x in range(10):
            for y in range(5):
                if x * y > 10:
                    result.append((x, y))

        return {
            x: complicated_transform(x)
            for x in long_generator_function(parameter)
            if x is not None
        }

        return (x**2 for x in range(10))

        unique_names = {user.name for user in users if user is not None}

.. code-block:: python

    No:
        result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]

        return (
            (x, y, z)
            for x in range(5)
            for y in range(5)
            if x != y
            for z in range(5)
            if y != z
        )

.. _s2.8-default-iterators-and-operators:

.. _default-iterators-operators:

2.8 默认迭代器和运算符
----------------------------

2.8 Default Iterators and Operators 

.. tab:: 中文

    对支持它们的类型（如列表、字典和文件）使用默认迭代器和运算符。

.. tab:: 英文

    Use default iterators and operators for types that support them, like lists, dictionaries, and files.

.. _s2.8.1-definition:
.. _281-definition:

.. _default-iterators-operators-definition:

2.8.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.8.1 Definition 

.. tab:: 中文

    容器类型，如字典和列表，定义默认迭代器和成员资格测试运算符（“in”和“not in”）。

.. tab:: 英文

    Container types, like dictionaries and lists, define default iterators and membership test operators ("in" and "not in").

.. _s2.8.2-pros:
.. _282-pros:

.. _default-iterators-operators-pros:

2.8.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.8.2 Pros 

.. tab:: 中文

    默认的迭代器和运算符简单高效。它们直接表达操作，无需额外的方法调用。使用默认运算符的函数是泛型函数。它可以用于任何支持该操作的类型。

.. tab:: 英文

    The default iterators and operators are simple and efficient. They express the operation directly, without extra method calls. A function that uses default operators is generic. It can be used with any type that supports the operation.

.. _s2.8.3-cons:
.. _283-cons:

.. _default-iterators-operators-cons:

2.8.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.8.3 Cons 

.. tab:: 中文

    你无法通过读取方法名称来判断对象的类型（除非变量有类型注释）。这也是一个优点。

.. tab:: 英文

    You can't tell the type of objects by reading the method names (unless the variable has type annotations). This is also an advantage.

.. _s2.8.4-decision:
.. _284-decision:

.. _default-iterators-operators-decision:

2.8.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.8.4 Decision 

.. tab:: 中文

    对于支持默认迭代器和运算符的类型，例如列表、字典和文件，请使用默认迭代器和运算符。内置类型也定义了迭代器方法。优先使用这些方法，而不是返回列表的方法，但迭代容器时不应对其进行修改。

.. tab:: 英文

    Use default iterators and operators for types that support them, like lists, dictionaries, and files. The built-in types define iterator methods, too. Prefer these methods to methods that return lists, except that you should not mutate a container while iterating over it.

.. code-block:: python

    Yes:  for key in adict: ...
          if obj in alist: ...
          for line in afile: ...
          for k, v in adict.items(): ...

.. code-block:: python

    No:   for key in adict.keys(): ...
          for line in afile.readlines(): ...

.. _s2.9-generators:
.. _29-generators:

.. _generators:

2.9 生成器
----------------------------

2.9 Generators 

.. tab:: 中文

    根据需要使用生成器。

.. tab:: 英文

    Use generators as needed.

.. _s2.9.1-definition:
.. _291-definition:

.. _generators-definition:

2.9.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.9.1 Definition 

.. tab:: 中文

    生成器函数返回一个迭代器，该迭代器每次执行 yield 语句时都会产生一个值。产生一个值后，生成器函数的运行时状态将被暂停，直到需要下一个值为止。

.. tab:: 英文

    A generator function returns an iterator that yields a value each time it executes a yield statement. After it yields a value, the runtime state of the generator function is suspended until the next value is needed.

.. _s2.9.2-pros:
.. _292-pros:

.. _generators-pros:

2.9.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.9.2 Pros 

.. tab:: 中文

    代码更简洁，因为每次调用时局部变量的状态和控制流都会被保留。生成器比一次性创建整个值列表的函数占用更少的内存。

.. tab:: 英文

    Simpler code, because the state of local variables and control flow are preserved for each call. A generator uses less memory than a function that creates an entire list of values at once.

.. _s2.9.3-cons:
.. _293-cons:

.. _generators-cons:

2.9.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.9.3 Cons 

.. tab:: 中文

    生成器中的局部变量将不会被垃圾收集，直到生成器耗尽或自身被垃圾收集为止。

.. tab:: 英文

    Local variables in the generator will not be garbage collected until the generator is either consumed to exhaustion or itself garbage collected.

.. _s2.9.4-decision:
.. _294-decision:

.. _generators-decision:

2.9.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.9.4 Decision 

.. tab:: 中文

    好的。在生成器函数的文档字符串中使用“Yields:”而不是“Returns:”。

    如果生成器管理的是高开销的资源，请务必强制清理。

    一个好的清理方法是用上下文管理器 `PEP-0533 <https://peps.python.org/pep-0533/>`_ 包装生成器。

.. tab:: 英文

    Fine. Use "Yields:" rather than "Returns:" in the docstring for generator functions.

    If the generator manages an expensive resource, make sure to force the clean up.

    A good way to do the clean up is by wrapping the generator with a context manager `PEP-0533 <https://peps.python.org/pep-0533/>`_ .

.. _s2.10-lambda-functions:
.. _210-lambda-functions:

.. _lambdas:

2.10 Lambda 函数
----------------------------

2.10 Lambda Functions 

.. tab:: 中文

    单行代码就行。建议使用生成器表达式，而不是 :code:`map()` 或 :code:`filter()`，并使用 :code:`lambda`。

.. tab:: 英文

    Okay for one-liners. Prefer generator expressions over :code:`map()` or :code:`filter()` with a :code:`lambda`.

.. _s2.10.1-definition:
.. _2101-definition:

.. _lambdas-definition:

2.10.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.10.1 Definition 

.. tab:: 中文

    Lambdas 在表达式中定义匿名函数，而不是语句。

.. tab:: 英文

    Lambdas define anonymous functions in an expression, as opposed to a statement.

.. _s2.10.2-pros:
.. _2102-pros:

.. _lambdas-pros:

2.10.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.10.2 Pros 

.. tab:: 中文

    方便的。

.. tab:: 英文

    Convenient.

.. _s2.10.3-cons:
.. _2103-cons:

.. _lambdas-cons:

2.10.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.10.3 Cons 

.. tab:: 中文

    比本地函数更难阅读和调试。缺少名称意味着堆栈跟踪更难理解。由于函数可能只包含一个表达式，因此表达能力有限。

.. tab:: 英文

    Harder to read and debug than local functions. The lack of names means stack traces are more difficult to understand. Expressiveness is limited because the function may only contain an expression.

.. _s2.10.4-decision:
.. _2104-decision:

.. _lambdas-decision:

2.10.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.10.4 Decision 

.. tab:: 中文

    允许使用 Lambda 表达式。如果 Lambda 函数内的代码跨越多行或长度超过 60-80 个字符，最好将其定义为常规的 :ref:`嵌套函数 <lexical-scoping>`。

    对于乘法等常见运算，请使用 :code:`operator` 模块中的函数，而不是 Lambda 函数。例如，建议使用 :code:`operator.mul` 而不是 :code:`lambda x, y: x * y`。

.. tab:: 英文

    Lambdas are allowed. If the code inside the lambda function spans multiple lines or is longer than 60-80 chars, it might be better to define it as a regular :ref:`nested function <lexical-scoping>`.

    For common operations like multiplication, use the functions from the :code:`operator` module instead of lambda functions. For example, prefer :code:`operator.mul` to :code:`lambda x, y: x * y`.

.. _s2.11-conditional-expressions:
.. _211-conditional-expressions:

.. _conditional-expressions:

2.11 条件表达式
----------------------------

2.11 Conditional Expressions 

.. tab:: 中文

    对于简单的情况来说还行。

.. tab:: 英文

    Okay for simple cases.

.. _s2.11.1-definition:
.. _2111-definition:

.. _conditional-expressions-definition:

2.11.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.11.1 Definition 

.. tab:: 中文

    条件表达式（有时也称为“三元运算符”）是一种为 if 语句提供更简洁语法的机制。例如：:code:`x = 1 if cond else 2` 。

.. tab:: 英文

    Conditional expressions (sometimes called a “ternary operator”) are mechanisms that provide a shorter syntax for if statements. For example: :code:`x = 1 if cond else 2`.

.. _s2.11.2-pros:
.. _2112-pros:

.. _conditional-expressions-pros:

2.11.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.11.2 Pros 

.. tab:: 中文

    比 if 语句更短、更方便。

.. tab:: 英文

    Shorter and more convenient than an if statement.

.. _s2.11.3-cons:
.. _2113-cons:

.. _conditional-expressions-cons:

2.11.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.11.3 Cons 

.. tab:: 中文

    可能比 if 语句更难读。如果表达式很长，可能难以找到条件。

.. tab:: 英文

    May be harder to read than an if statement. The condition may be difficult to locate if the expression is long.

.. _s2.11.4-decision:
.. _2114-decision:

.. _conditional-expressions-decision:

2.11.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.11.4 Decision 

.. tab:: 中文

    适用于简单情况。每个部分必须放在一行：真值表达式、if 表达式、else 表达式。如果情况更复杂，请使用完整的 if 语句。

.. tab:: 英文

    Okay to use for simple cases. Each portion must fit on one line: true-expression, if-expression, else-expression. Use a complete if statement when things get more complicated.

.. code-block:: python

    Yes:
        one_line = 'yes' if predicate(value) else 'no'
        slightly_split = ('yes' if predicate(value)
                        else 'no, nein, nyet')
        the_longest_ternary_style_that_can_be_done = (
            'yes, true, affirmative, confirmed, correct'
            if predicate(value)
            else 'no, false, negative, nay')

.. code-block:: python

    No:
        bad_line_breaking = ('yes' if predicate(value) else
                            'no')
        portion_too_long = ('yes'
                            if some_long_module.some_long_predicate_function(
                                really_long_variable_name)
                            else 'no, false, negative, nay')

.. _s2.12-default-argument-values:
.. _212-default-argument-values:

.. _default-arguments:

2.12 默认参数值
----------------------------

2.12 Default Argument Values 

.. tab:: 中文

    大多数情况下都可以。

.. tab:: 英文

    Okay in most cases.

.. _s2.12.1-definition:
.. _2121-definition:

.. _default-arguments-definition:

2.12.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.12.1 Definition 

.. tab:: 中文

    您可以在函数参数列表的末尾指定变量的值，例如：:code:`def foo(a, b=0):`。如果仅使用一个参数调用 :code:`foo`，则 :code:`b` 设置为 0。如果使用两个参数调用，则 :code:`b` 具有第二个参数的值。

.. tab:: 英文

    You can specify values for variables at the end of a function's parameter list, e.g., :code:`def foo(a, b=0):`. If :code:`foo` is called with only one argument, :code:`b` is set to 0. If it is called with two arguments, :code:`b` has the value of the second argument.

.. _s2.12.2-pros:
.. _2122-pros:

.. _default-arguments-pros:

2.12.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.12.2 Pros 

.. tab:: 中文

    通常，你会遇到一个使用大量默认值的函数，但在极少数情况下，你会想要覆盖这些默认值。默认参数值提供了一种简单的方法来实现这一点，而无需为这些罕见的例外情况定义大量的函数。由于 Python 不支持重载方法/函数，默认参数是一种“伪造(faking)”重载行为的简单方法。

.. tab:: 英文

    Often you have a function that uses lots of default values, but on rare occasions you want to override the defaults. Default argument values provide an easy way to do this, without having to define lots of functions for the rare exceptions. As Python does not support overloaded methods/functions, default arguments are an easy way of "faking" the overloading behavior.

.. _s2.12.3-cons:
.. _2123-cons:

.. _default-arguments-cons:

2.12.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.12.3 Cons 

.. tab:: 中文

    默认参数在模块加载时会被求值一次。如果参数是可变对象（例如列表或字典），则可能会导致问题。如果函数修改了该对象（例如，将一个项附加到列表中），则默认值也会被修改。

.. tab:: 英文

    Default arguments are evaluated once at module load time. This may cause problems if the argument is a mutable object such as a list or a dictionary. If the function modifies the object (e.g., by appending an item to a list), the default value is modified.

.. _s2.12.4-decision:
.. _2124-decision:

.. _default-arguments-decision:

2.12.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.12.4 Decision 

.. tab:: 中文

    可以使用，但需要注意以下事项：

    请勿在函数或方法定义中使用可变对象作为默认值。

    .. code-block:: python

        Yes: def foo(a, b=None):
                if b is None:
                    b = []
        Yes: def foo(a, b: Sequence | None = None):
                if b is None:
                    b = []
        Yes: def foo(a, b: Sequence = ()):  # 空元组可以，因为元组是不可变的.
                ...

    .. code-block:: python

        from absl import flags
        _FOO = flags.DEFINE_string(...)

        No:  def foo(a, b=[]):
                ...
        No:  def foo(a, b=time.time()):  # “b” 是否应该代表该模块的加载时间？
                ...
        No:  def foo(a, b=_FOO.value):  # sys.argv 尚未被解析...
                ...
        No:  def foo(a, b: Mapping = {}):  # 仍可能传递给未经检查的代码。
                ...


.. tab:: 英文

    Okay to use with the following caveat:

    Do not use mutable objects as default values in the function or method definition.

    .. code-block:: python

        Yes: def foo(a, b=None):
                if b is None:
                    b = []
        Yes: def foo(a, b: Sequence | None = None):
                if b is None:
                    b = []
        Yes: def foo(a, b: Sequence = ()):  # Empty tuple OK since tuples are immutable.
                ...

    .. code-block:: python

        from absl import flags
        _FOO = flags.DEFINE_string(...)

        No:  def foo(a, b=[]):
                ...
        No:  def foo(a, b=time.time()):  # Is `b` supposed to represent when this module was loaded?
                ...
        No:  def foo(a, b=_FOO.value):  # sys.argv has not yet been parsed...
                ...
        No:  def foo(a, b: Mapping = {}):  # Could still get passed to unchecked code.
                ...

.. _s2.13-properties:
.. _213-properties:

.. _properties:

2.13 属性
----------------------------

2.13 Properties 

.. tab:: 中文

    属性可用于控制需要简单计算或逻辑的属性的获取或设置。属性的实现必须符合常规属性访问的一般期望：简洁、直接且不令人意外。

.. tab:: 英文

    Properties may be used to control getting or setting attributes that require trivial computations or logic. Property implementations must match the general expectations of regular attribute access: that they are cheap, straightforward, and unsurprising.

.. _s2.13.1-definition:
.. _2131-definition:

.. _properties-definition:

2.13.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.13.1 Definition 

.. tab:: 中文

    将获取和设置属性的方法调用包装为标准属性访问的方式。

.. tab:: 英文

    A way to wrap method calls for getting and setting an attribute as a standard attribute access.

.. _s2.13.2-pros:
.. _2132-pros:

.. _properties-pros:

2.13.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.13.2 Pros 

.. tab:: 中文

    * 允许使用属性访问和赋值 API，而不是 :ref:`getter 和 setter <getters-and-setters>` 方法调用。
    * 可用于将属性设为只读。
    * 允许延迟计算。
    * 当类的内部结构独立于类的使用者而发展时，提供一种维护类的公共接口的方法。

.. tab:: 英文

    * Allows for an attribute access and assignment API rather than :ref:`getter and setter <getters-and-setters>` method calls.
    * Can be used to make an attribute read-only.
    * Allows calculations to be lazy.
    * Provides a way to maintain the public interface of a class when the internals evolve independently of class users.

.. _s2.13.3-cons:
.. _2133-cons:

.. _properties-cons:

2.13.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.13.3 Cons 

.. tab:: 中文

    * 可以像运算符重载一样隐藏副作用。
    * 可能会使子类感到困惑。

.. tab:: 英文

    * Can hide side-effects much like operator overloading.
    * Can be confusing for subclasses.

.. _s2.13.4-decision:
.. _2134-decision:

.. _properties-decision:

2.13.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.13.4 Decision 

.. tab:: 中文

    允许使用属性，但与运算符重载类似，应仅在必要时使用，并且应符合典型属性访问的预期；否则，请遵循 :ref:`getters 和 setters <getters-and-setters>` 规则。

    例如，不允许使用属性简单地同时获取和设置内部属性：因为没有进行任何计算，因此该属性是不必要的（:ref:`改为将属性公开 <getters-and-setters>`）。相比之下，允许使用属性来控制属性访问或计算 *简单* 派生的值：其逻辑简单且不足为奇。

    应使用 :code:`@property` :ref:`装饰器 <s2.17-function-and-method-decorators>` 创建属性。手动实现属性描述符被视为一项 :ref:`强大功能 <power-features>`。

    属性的继承可能不明显。请勿使用属性来实现子类可能想要重写和扩展的计算。

.. tab:: 英文

    Properties are allowed, but, like operator overloading, should only be used when necessary and match the expectations of typical attribute access; follow the :ref:`getters 和 setters <getters-and-setters>` rules otherwise.

    For example, using a property to simply both get and set an internal attribute isn't allowed: there is no computation occurring, so the property is unnecessary (:ref:`make the attribute public instead <getters-and-setters>`). In comparison, using a property to control attribute access or to calculate a *trivially* derived value is allowed: the logic is simple and unsurprising.

    Properties should be created with the :code:`@property` :ref:`decorator <s2.17-function-and-method-decorators>` Manually implementing a property descriptor is considered a :ref:`power feature <power-features>`.

    Inheritance with properties can be non-obvious. Do not use properties to implement computations a subclass may ever want to override and extend.

.. _s2.14-truefalse-evaluations:
.. _214-truefalse-evaluations:

.. _truefalse-evaluations:

2.14 真/假判断
----------------------------

2.14 True/False Evaluations 

.. tab:: 中文

    如果可能的话，使用“隐式”错误（有一些警告）。

.. tab:: 英文

    Use the "implicit" false if at all possible (with a few caveats).

.. _s2.14.1-definition:
.. _2141-definition:

.. _truefalse-evaluations-definition:

2.14.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.14.1 Definition 

.. tab:: 中文

    Python 在布尔上下文中将某些值计算为 :code:`False`。一个简单的“经验法则”是，所有“空”值都被视为 false，因此 :code:`0、None、[]、{}、''` 在布尔上下文中均被计算为 false。

.. tab:: 英文

    Python evaluates certain values as :code:`False` when in a boolean context. A quick "rule of thumb" is that all "empty" values are considered false, so :code:`0, None, [], {}, ''` all evaluate as false in a boolean context.

.. _s2.14.2-pros:
.. _2142-pros:

.. _truefalse-evaluations-pros:

2.14.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.14.2 Pros 

.. tab:: 中文

    使用 Python 布尔值来设置条件更易于阅读，且不易出错。在大多数情况下，它们的速度也更快。

.. tab:: 英文

    Conditions using Python booleans are easier to read and less error-prone. In most cases, they're also faster.

.. _s2.14.3-cons:
.. _2143-cons:

.. _truefalse-evaluations-cons:

2.14.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.14.3 Cons 

.. tab:: 中文

    对于 C/C++ 开发人员来说可能看起来很奇怪。

.. tab:: 英文

    May look strange to C/C++ developers.

.. _s2.14.4-decision:
.. _2144-decision:

.. _truefalse-evaluations-decision:

2.14.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.14.4 Decision 

.. tab:: 中文

    尽可能使用“隐式”假值判断，例如使用 :code:`if foo:` 而不是 :code:`if foo != []:`。不过，也有一些注意事项需要留意：

    -   检查一个值是否为 :code:`None` 时，应始终使用 :code:`if foo is None:` （或 :code:`is not None` ）。
        例如，在判断一个默认值为 :code:`None` 的变量或参数是否被赋予了其他值时。其他值可能在布尔上下文中也会被判断为假！

    -   永远不要通过 :code:`==` 将布尔变量与 :code:`False` 进行比较，应使用 :code:`if not x:`。
        如果你需要区分 :code:`False` 和 :code:`None`，可以链式组合表达式，如 :code:`if not x and x is not None:`。

    -   对于序列（字符串、列表、元组），应利用空序列为假值的事实，因此使用 :code:`if seq:` 和 :code:`if not seq:` 比使用 :code:`if len(seq):` 和 :code:`if not len(seq):` 更佳。

    -   在处理整数时，隐式假值可能弊大于利（例如，可能会误将 :code:`None` 当作 0 处理）。你可以将已知为整数（且不是 :code:`len()` 的结果）的值与整数 0 进行比较。

        .. code-block:: python

            Yes: if not users:
                    print('no users')

                 if i % 10 == 0:
                    self.handle_multiple_of_ten()

                 def f(x=None):
                    if x is None:
                        x = []

        .. code-block:: python

            No: if len(users) == 0:
                    print('no users')
            
                if not i % 10:
                    self.handle_multiple_of_ten()
            
                def f(x=None):
                    x = x or []

    -   注意，:code:`'0'` （即字符串形式的 :code:`0` ）在布尔上下文中会被视为真值。

    -   注意，Numpy 数组在隐式布尔上下文中可能会抛出异常。判断 :code:`np.array` 是否为空时，推荐使用其 :code:`.size` 属性（例如 :code:`if not users.size`）。


.. tab:: 英文

    Use the "implicit" false if possible, e.g., :code:`if foo:` rather than :code:`if foo != []:`. There are a few caveats that you should keep in mind though:

    -   Always use :code:`if foo is None:` (or :code:`is not None`) to check for a :code:`None` value.
        E.g., when testing whether a variable or argument that defaults to :code:`None`
        was set to some other value. The other value might be a value that's false
        in a boolean context!

    -   Never compare a boolean variable to :code:`False` using :code:`==`. Use :code:`if not x:`
        instead. If you need to distinguish :code:`False` from :code:`None` then chain the
        expressions, such as :code:`if not x and x is not None:`.

    -   For sequences (strings, lists, tuples), use the fact that empty sequences
        are false, so :code:`if seq:` and :code:`if not seq:` are preferable to :code:`if len(seq):`
        and :code:`if not len(seq):` respectively.

    -   When handling integers, implicit false may involve more risk than benefit
        (i.e., accidentally handling :code:`None` as 0). You may compare a value which is
        known to be an integer (and is not the result of :code:`len()`) against the
        integer 0.

        .. code-block:: python

            Yes: if not users:
                    print('no users')

                if i % 10 == 0:
                    self.handle_multiple_of_ten()

                def f(x=None):
                    if x is None:
                        x = []

        .. code-block:: python

            No:  if len(users) == 0:
                    print('no users')
        
                if not i % 10:
                    self.handle_multiple_of_ten()
        
                def f(x=None):
                    x = x or []

    -   Note that :code:`'0'` (i.e., :code:`0` as string) evaluates to true.

    -   Note that Numpy arrays may raise an exception in an implicit boolean
        context. Prefer the :code:`.size` attribute when testing emptiness of a :code:`np.array` (e.g. :code:`if not users.size`).

.. _s2.16-lexical-scoping:
.. _216-lexical-scoping:

.. _lexical-scoping:

2.16 词法作用域
----------------------------

2.16 Lexical Scoping 

.. tab:: 中文

    可以用。

.. tab:: 英文

    Okay to use.

.. _s2.16.1-definition:
.. _2161-definition:

.. _lexical-scoping-definition:

2.16.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.16.1 Definition 

.. tab:: 中文

    嵌套的 Python 函数可以引用封闭函数中定义的变量，但不能赋值给它们。变量绑定使用词法作用域进行解析，即基于静态程序文本。在代码块中对名称的任何赋值都会导致 Python 将所有对该名称的引用视为局部变量，即使使用先于赋值。如果出现全局声明，则该名称将被视为全局变量。

    此功能的一个使用示例如下：

    .. code-block:: python

        def get_adder(summand1: float) -> Callable[[float], float]:
            """返回将数字添加到给定数字的函数."""
            def adder(summand2: float) -> float:
                return summand1 + summand2
        
            return adder

.. tab:: 英文

    A nested Python function can refer to variables defined in enclosing functions,
    but cannot assign to them. Variable bindings are resolved using lexical scoping,
    that is, based on the static program text. Any assignment to a name in a block
    will cause Python to treat all references to that name as a local variable, even
    if the use precedes the assignment. If a global declaration occurs, the name is
    treated as a global variable.

    An example of the use of this feature is:

    .. code-block:: python

        def get_adder(summand1: float) -> Callable[[float], float]:
            """Returns a function that adds numbers to a given number."""
            def adder(summand2: float) -> float:
                return summand1 + summand2
        
            return adder

.. _s2.16.2-pros:
.. _2162-pros:

.. _lexical-scoping-pros:

2.16.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.16.2 Pros 

.. tab:: 中文

    通常会导致代码更清晰、更优雅。尤其适合经验丰富的 Lisp 和 Scheme（以及 Haskell、ML 等等）程序员。

.. tab:: 英文

    Often results in clearer, more elegant code. Especially comforting to experienced Lisp and Scheme (and Haskell and ML and ...) programmers.

.. _s2.16.3-cons:
.. _2163-cons:

.. _lexical-scoping-cons:

2.16.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.16.3 Cons 

.. tab:: 中文

    可能会导致令人困惑的错误，例如基于 `PEP-0227 <https://peps.python.org/pep-0227/>`_ 的这个示例：

    .. code-block:: python

        i = 4
        def foo(x: Iterable[int]):
            def bar():
                print(i, end='')
            # ...
            # 这里有一堆代码
            # ...
            for i in x:  # 阿哈, i *is* local to foo, so this is what bar sees
                print(i, end='')
            bar()

    So :code:`foo([1, 2, 3])` will print :code:`1 2 3 3`, not :code:`1 2 3 4`.

.. tab:: 英文

    Can lead to confusing bugs, such as this example based on `PEP-0227 <https://peps.python.org/pep-0227/>`_:

    .. code-block:: python

        i = 4
        def foo(x: Iterable[int]):
            def bar():
                print(i, end='')
            # ...
            # A bunch of code here
            # ...
            for i in x:  # Ah, i *is* local to foo, so this is what bar sees
                print(i, end='')
            bar()

    So :code:`foo([1, 2, 3])` will print :code:`1 2 3 3`, not :code:`1 2 3 4`.

.. _s2.16.4-decision:
.. _2164-decision:

.. _lexical-scoping-decision:

2.16.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.16.4 Decision 

.. tab:: 中文

    可以用。

.. tab:: 英文

    Okay to use.

.. _s2.17-function-and-method-decorators:
.. _217-function-and-method-decorators:
.. _function-and-method-decorators:

.. _decorators:

2.17 函数和方法装饰器
----------------------------

2.17 Function and Method Decorators 

.. tab:: 中文

    当装饰器有明显优势时，请谨慎使用。避免使用 :code:`staticmethod` 并限制使用 :code:`classmethod`。

.. tab:: 英文

    Use decorators judiciously when there is a clear advantage. Avoid :code:`staticmethod` and limit use of :code:`classmethod`.

.. _s2.17.1-definition:
.. _2171-definition:

.. _decorators-definition:

2.17.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.17.1 Definition 

.. tab:: 中文

    `函数和方法的装饰器 <https://docs.python.org/3/glossary.html#term-decorator>`_（又称“ :code:`@` 符号 ”）。一个常见的装饰器是 :code:`@property`，用于将普通方法转换为动态计算的属性。然而，装饰器语法也允许用户自定义装饰器。具体来说，对于某个函数 :code:`my_decorator`，如下所示：

    .. code-block:: python

        class C:
            @my_decorator
            def method(self):
                # method body ...

    相当于:

    .. code-block:: python

        class C:
            def method(self):
                # method body ...

            method = my_decorator(method)

.. tab:: 英文

    `Decorators for Functions and Methods <https://docs.python.org/3/glossary.html#term-decorator>`_
    (a.k.a "the :code:`@` notation"). One common decorator is :code:`@property`, used for
    converting ordinary methods into dynamically computed attributes. However, the
    decorator syntax allows for user-defined decorators as well. Specifically, for
    some function :code:`my_decorator`, this:

    .. code-block:: python

        class C:
            @my_decorator
            def method(self):
                # method body ...

    is equivalent to:

    .. code-block:: python

        class C:
            def method(self):
                # method body ...

            method = my_decorator(method)

.. _s2.17.2-pros:
.. _2172-pros:

.. _decorators-pros:

2.17.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.17.2 Pros 

.. tab:: 中文

    优雅地指定方法上的一些转换；转换可能会消除一些重复的代码，强制执行不变量等。

.. tab:: 英文

    Elegantly specifies some transformation on a method; the transformation might eliminate some repetitive code, enforce invariants, etc.

.. _s2.17.3-cons:
.. _2173-cons:

.. _decorators-cons:

2.17.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.17.3 Cons 

.. tab:: 中文

    装饰器可以对函数的参数或返回值执行任意操作，从而导致令人意外的隐式行为。此外，装饰器在对象定义时执行。对于模块级对象（类、模块函数等），这发生在导入时。装饰器代码中的错误几乎无法恢复。

.. tab:: 英文

    Decorators can perform arbitrary operations on a function's arguments or return values, resulting in surprising implicit behavior. Additionally, decorators execute at object definition time. For module-level objects (classes, module functions, ...) this happens at import time. Failures in decorator code are pretty much impossible to recover from.

.. _s2.17.4-decision:
.. _2174-decision:

.. _decorators-decision:

2.17.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.17.4 Decision 

.. tab:: 中文

    当装饰器有明显优势时，请谨慎使用。装饰器应遵循与函数相同的导入和命名准则。装饰器文档字符串应清晰地声明该函数是一个装饰器。请为装饰器编写单元测试。

    避免在装饰器本身中引入外部依赖（例如，不要依赖文件、套接字、数据库连接等），因为这些依赖在装饰器运行时可能不可用（在导入时，可能是从 :code:`pydoc` 或其他工具导入）。使用有效参数调用的装饰器应（尽可能）保证在所有情况下都能成功调用。

    装饰器是“顶层代码”的一种特殊情况 - 更多讨论请参阅 :ref:`main <s3.17-main>`。

    除非为了与现有库中定义的 API 集成而被迫使用 :code:`staticmethod`，否则切勿使用 :code:`staticmethod`。请改为编写模块级函数。

    仅在编写命名构造函数或修改必要的全局状态（例如进程范围的缓存）的特定于类的例程时使用 :code:`classmethod`。

.. tab:: 英文

    Use decorators judiciously when there is a clear advantage. Decorators should follow the same import and naming guidelines as functions. A decorator docstring should clearly state that the function is a decorator. Write unit tests for decorators.

    Avoid external dependencies in the decorator itself (e.g. don't rely on files, sockets, database connections, etc.), since they might not be available when the decorator runs (at import time, perhaps from :code:`pydoc` or other tools). A decorator that is called with valid parameters should (as much as possible) be guaranteed to succeed in all cases.

    Decorators are a special case of "top-level code" - see :ref:`main <s3.17-main>` for
    more discussion.

    Never use :code:`staticmethod` unless forced to in order to integrate with an API defined in an existing library. Write a module-level function instead.

    Use :code:`classmethod` only when writing a named constructor, or a class-specific routine that modifies necessary global state such as a process-wide cache.

.. _s2.18-threading:
.. _218-threading:

.. _threading:

2.18 线程
----------------------------

2.18 Threading 

.. tab:: 中文

    不要依赖内置类型的原子性。

    虽然 Python 的内置数据类型（例如字典）似乎具有原子操作，但在某些情况下它们并非原子操作（例如，如果 :code:`__hash__` 或 :code:`__eq__` 被实现为 Python 方法），则不应依赖它们的原子性。也不应该依赖原子变量赋值（因为这反过来又依赖于字典）。

    使用 :code:`queue` 模块的 :code:`Queue` 数据类型作为线程间数据通信的首选方式。否则，请使用 :code:`threading` 模块及其锁定原语。优先使用条件变量和 :code:`threading.Condition`，而不是使用低级锁。

.. tab:: 英文

    Do not rely on the atomicity of built-in types.

    While Python's built-in data types such as dictionaries appear to have atomic operations, there are corner cases where they aren't atomic (e.g. if :code:`__hash__` or :code:`__eq__` are implemented as Python methods) and their atomicity should not be relied upon. Neither should you rely on atomic variable assignment (since this in turn depends on dictionaries).

    Use the :code:`queue` module's :code:`Queue` data type as the preferred way to communicate data between threads. Otherwise, use the :code:`threading` module and its locking primitives. Prefer condition variables and :code:`threading.Condition` instead of using lower-level locks.

.. _s2.19-power-features:
.. _219-power-features:

.. _power-features:

2.19 强大的功能
----------------------------

2.19 Power Features 

.. tab:: 中文

    避免这些功能。

.. tab:: 英文

    Avoid these features.

.. _s2.19.1-definition:
.. _2191-definition:

.. _power-features-definition:

2.19.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.19.1 Definition 

.. tab:: 中文

    Python 是一种非常灵活的语言，它为您提供了许多奇特的功能，例如自定义元类、访问字节码、动态编译、动态继承、对象重新父级、导入黑客、反射（例如 :code:`getattr()` 的一些用途）、修改系统内部、 :code:`__del__` 方法实现自定义清理等。

.. tab:: 英文

    Python is an extremely flexible language and gives you many fancy features such as custom metaclasses, access to bytecode, on-the-fly compilation, dynamic inheritance, object reparenting, import hacks, reflection (e.g. some uses of :code:`getattr()`), modification of system internals, :code:`__del__` methods implementing customized cleanup, etc.

.. _s2.19.2-pros:
.. _2192-pros:

.. _power-features-pros:

2.19.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.19.2 Pros 

.. tab:: 中文

    这些都是强大的语言特性。它们可以让你的代码更加紧凑。

.. tab:: 英文

    These are powerful language features. They can make your code more compact.

.. _s2.19.3-cons:
.. _2193-cons:

.. _power-features-cons:

2.19.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.19.3 Cons 

.. tab:: 中文

    当这些“酷炫”的功能并非绝对必要的时候，人们很容易就会去使用这些功能。然而，如果代码中使用了不常见的功能，阅读、理解和调试起来就会更加困难。乍一看（对原作者来说）似乎并非如此，但当你重新审视这些代码时，你会发现，它们往往比那些更长但更简单的代码更难理解。

.. tab:: 英文

    It's very tempting to use these "cool" features when they're not absolutely necessary. It's harder to read, understand, and debug code that's using unusual features underneath. It doesn't seem that way at first (to the original author), but when revisiting the code, it tends to be more difficult than code that is longer but is straightforward.

.. _s2.19.4-decision:
.. _2194-decision:

.. _power-features-decision:

2.19.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.19.4 Decision 

.. tab:: 中文

    避免在代码中使用这些功能。

    内部使用这些功能的标准库模块和类是可以使用的（例如：:code:`abc.ABCMeta` 、:code:`dataclasses` 和 :code:`enum`）。

.. tab:: 英文

    Avoid these features in your code.

    Standard library modules and classes that internally use these features are okay to use (for example, :code:`abc.ABCMeta`, :code:`dataclasses`, and :code:`enum`).

.. _s2.20-modern-python:
.. _220-modern-python:
.. _from-future-imports:

.. _modern-python:

2.20 现代 Python：从 ``__future__`` 导入
--------------------------------------------------------

2.20 Modern Python: from ``__future__`` imports

.. tab:: 中文

    新的语言版本语义变化可能会受到特殊未来导入的控制，以便在早期运行时按文件启用它们。

.. tab:: 英文

    New language version semantic changes may be gated behind a special future import to enable them on a per-file basis within earlier runtimes.

.. _s2.20.1-definition:
.. _2201-definition:

.. _modern-python-definition:

2.20.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.20.1 Definition 

.. tab:: 中文

    能够通过 :code:`from __future__ import` 语句启用一些更现代的功能，从而可以提前使用预期的未来 Python 版本中的功能。

.. tab:: 英文

    Being able to turn on some of the more modern features via :code:`from __future__ import` statements allows early use of features from expected future Python versions.

.. _s2.20.2-pros:
.. _2202-pros:

.. _modern-python-pros:

2.20.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.20.2 Pros 

.. tab:: 中文

    事实证明，这可以使运行时版本升级更加顺畅，因为可以逐个文件进行更改，同时声明兼容性并防止这些文件中出现回归问题。现代代码更易于维护，因为它不太可能积累技术债务，而这些债务在未来的运行时升级中会造成问题。

.. tab:: 英文

    This has proven to make runtime version upgrades smoother as changes can be made on a per-file basis while declaring compatibility and preventing regressions within those files. Modern code is more maintainable as it is less likely to accumulate technical debt that will be problematic during future runtime upgrades.

.. _s2.20.3-cons:
.. _2203-cons:

.. _modern-python-cons:

2.20.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.20.3 Cons 

.. tab:: 中文

    此类代码可能无法在引入所需的 Future 语句之前的旧解释器版本上运行。这种需求在支持极其多样化环境的项目中更为常见。

.. tab:: 英文

    Such code may not work on very old interpreter versions prior to the introduction of the needed future statement. The need for this is more common in projects supporting an extremely wide variety of environments.

.. _s2.20.4-decision:
.. _2204-decision:

.. _modern-python-decision:

2.20.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.20.4 Decision 


从 ``__future__`` 导入
""""""""""""""""""""""""""""""""""""

from ``__future__`` imports

.. tab:: 中文

    鼓励使用 :code:`from __future__ import` 语句。它允许给定的源文件立即使用更现代的 Python 语法特性。当您不再需要运行隐藏在 :code:`__future__` 导入语句后面的版本时，请随时删除这些代码行。

    在可能在 3.5 版（而非 >= 3.7 版）上执行的代码中，导入：

    .. code-block:: python
        
        from __future__ import generator_stop

    更多信息请阅读 `Python Future 语句定义 <https://docs.python.org/3/library/__future__.html>`_ 文档。

    除非您确信代码只会在足够现代化的环境中运行，否则请勿删除这些导入语句。即使您目前没有在代码中使用特定 Future 导入语句启用的功能，将其保留在文件中也可以防止以后对代码的修改无意中依赖于旧的行为。

    请根据需要使用其他 :code:`from __future__` 导入语句。

.. tab:: 英文

    Use of :code:`from __future__ import` statements is encouraged. It allows a given source file to start using more modern Python syntax features today. Once you no longer need to run on a version where the features are hidden behind a :code:`__future__` import, feel free to remove those lines.

    In code that may execute on versions as old as 3.5 rather than >= 3.7, import:

    .. code-block:: python
        
        from __future__ import generator_stop

    For more information read the `Python future statement definitions <https://docs.python.org/3/library/__future__.html>`_ documentation.

    Please don't remove these imports until you are confident the code is only ever used in a sufficiently modern environment. Even if you do not currently use the feature a specific future import enables in your code today, keeping it in place in the file prevents later modifications of the code from inadvertently depending on the older behavior.

    Use other :code:`from __future__` import statements as you see fit.

.. _s2.21-type-annotated-code:
.. _s2.21-typed-code:
.. _221-type-annotated-code:
.. _typed-code:

.. _typed-code:

2.21 带类型注释的代码
----------------------------

2.21 Type Annotated Code 

.. tab:: 中文

    您可以使用 `类型提示 <https://docs.python.org/3/library/typing.html>`_ 为 Python 代码添加注释。在构建时，请使用 `pytype <https://github.com/google/pytype>`_ 等类型检查工具对代码进行类型检查。在大多数情况下，如果可行，类型注释都包含在源文件中。对于第三方或扩展模块，注释可以包含在 `stub .pyi 文件 <https://peps.python.org/pep-0484/#stub-filespytype>`_ 中。

    .. admonition:: 译注

        `mypy <https://hellowac.github.io/mypy-zh-cn/>`_ 是一个python官方支持的静态类型检查工具, 可以较好的结合各类IDE来检查你写的代码的静态类型。

.. tab:: 英文

    You can annotate Python code with `type hints <https://docs.python.org/3/library/typing.html>`_ . Type-check the code at build time with a type checking tool like `pytype <https://github.com/google/pytype>`_ . In most cases, when feasible, type annotations are in source files. For third-party or extension modules, annotations can be in `stub .pyi files <https://peps.python.org/pep-0484/#stub-filespytype>`_ .


.. _s2.21.1-definition:
.. _2211-definition:

.. _typed-code-definition:

2.21.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.21.1 Definition 

.. tab:: 中文

    类型注释（或“类型提示”）用于函数或方法的参数和返回值：

    .. code-block:: python

        def func(a: int) -> list[int]:

    您还可以使用类似的语法声明变量的类型：

    .. code-block:: python

        a: SomeType = some_func()

.. tab:: 英文

    Type annotations (or "type hints") are for function or method arguments and return values:

    .. code-block:: python

        def func(a: int) -> list[int]:

    You can also declare the type of a variable using similar syntax:

    .. code-block:: python

        a: SomeType = some_func()


.. _s2.21.2-pros:
.. _2212-pros:

.. _typed-code-pros:

2.21.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.21.2 Pros 

.. tab:: 中文

    类型注解可以提升代码的可读性和可维护性。类型检查器会将许多运行时错误转换为构建时错误，从而降低您使用 :ref:`强大功能 <power-features>` 的能力。

.. tab:: 英文

    Type annotations improve the readability and maintainability of your code. The type checker will convert many runtime errors to build-time errors, and reduce your ability to use :ref:`Power Features <power-features>`.

.. _s2.21.3-cons:
.. _2213-cons:

.. _typed-code-cons:

2.21.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.21.3 Cons 

.. tab:: 中文

    您必须保持类型声明的更新。您可能会看到一些您认为是有效代码的类型错误。使用 `类型检查器 <https://github.com/google/pytype>`_ 可能会降低您使用 :ref:`强大功能 <power-features>` 的能力。

.. tab:: 英文

    You will have to keep the type declarations up to date. You might see type errors that you think are valid code. Use of a  `type checker <https://github.com/google/pytype>`_  may reduce your ability to use :ref:`Power Features <power-features>` .

.. _s2.21.4-decision:
.. _2214-decision:

.. _typed-code-decision:

2.21.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.21.4 Decision 

.. tab:: 中文

    强烈建议您在更新代码时启用 Python 类型分析。添加或修改公共 API 时，请在构建系统中添加类型注解并启用通过 pytype 进行检查的功能。由于静态分析对于 Python 来说相对较新，我们承认一些不良副作用（例如错误的类型推断）可能会阻碍某些项目的采用。在这种情况下，我们鼓励作者在 BUILD 文件或代码中添加 TODO 注释或指向 bug 的链接，以描述当前阻碍类型注解采用的问题。

.. tab:: 英文

    You are strongly encouraged to enable Python type analysis when updating code. When adding or modifying public APIs, include type annotations and enable checking via pytype in the build system. As static analysis is relatively new to Python, we acknowledge that undesired side-effects (such as wrongly inferred types) may prevent adoption by some projects. In those situations, authors are encouraged to add a comment with a TODO or link to a bug describing the issue(s) currently preventing type annotation adoption in the BUILD file or in the code itself as appropriate.