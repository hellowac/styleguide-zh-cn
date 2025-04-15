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

.. tab:: 英文

* Breaks encapsulation: Such design can make it hard to achieve valid
  objectives. For example, if global state is used to manage a database
  connection, then connecting to two different databases at the same time
  (such as for computing differences during a migration) becomes difficult.
  Similar problems easily arise with global registries.

* Has the potential to change module behavior during the import, because
  assignments to global variables are done when the module is first imported.

.. _s2.5.4-decision:
.. _254-decision:

.. _global-variables-decision:

2.5.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.5.4 Decision 

.. tab:: 中文

.. tab:: 英文

Avoid mutable global state.

In those rare cases where using global state is warranted, mutable global
entities should be declared at the module level or as a class attribute and made
internal by prepending an `_` to the name. If necessary, external access to
mutable global state must be done through public functions or class methods. See
[Naming](#s3.16-naming) below. Please explain the design reasons why mutable
global state is being used in a comment or a doc linked to from a comment.

Module-level constants are permitted and encouraged. For example:
`_MAX_HOLY_HANDGRENADE_COUNT = 3` for an internal use constant or
`SIR_LANCELOTS_FAVORITE_COLOR = "blue"` for a public API constant. Constants
must be named using all caps with underscores. See [Naming](#s3.16-naming)
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

.. tab:: 英文

They are fine with some caveats. Avoid nested functions or classes except when
closing over a local value other than :code:`self` or :code:`cls`. Do not nest a function
just to hide it from users of a module. Instead, prefix its name with an ``_`` at
the module level so that it can still be accessed by tests.

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

.. tab:: 英文

Okay to use for simple cases.

.. _s2.7.1-definition:
.. _271-definition:

.. _comprehensions-definition:

2.7.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.7.1 Definition 

.. tab:: 中文

.. tab:: 英文

List, Dict, and Set comprehensions as well as generator expressions provide a
concise and efficient way to create container types and iterators without
resorting to the use of traditional loops, :code:`map()`, :code:`filter()`, or :code:`lambda`.

.. _s2.7.2-pros:
.. _272-pros:

.. _comprehensions-pros:

2.7.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.7.2 Pros 

.. tab:: 中文

.. tab:: 英文

Simple comprehensions can be clearer and simpler than other dict, list, or set
creation techniques. Generator expressions can be very efficient, since they
avoid the creation of a list entirely.

.. _s2.7.3-cons:
.. _273-cons:

.. _comprehensions-cons:

2.7.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.7.3 Cons 

.. tab:: 中文

.. tab:: 英文

Complicated comprehensions or generator expressions can be hard to read.

.. _s2.7.4-decision:
.. _274-decision:

.. _comprehensions-decision:

2.7.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.7.4 Decision 

.. tab:: 中文

.. tab:: 英文

Comprehensions are allowed, however multiple :code:`for` clauses or filter expressions
are not permitted. Optimize for readability, not conciseness.

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

.. tab:: 英文

Use default iterators and operators for types that support them, like lists, dictionaries, and files.

.. _s2.8.1-definition:
.. _281-definition:

.. _default-iterators-operators-definition:

2.8.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.8.1 Definition 

.. tab:: 中文

.. tab:: 英文

Container types, like dictionaries and lists, define default iterators and membership test operators ("in" and "not in").

.. _s2.8.2-pros:
.. _282-pros:

.. _default-iterators-operators-pros:

2.8.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.8.2 Pros 

.. tab:: 中文

.. tab:: 英文

The default iterators and operators are simple and efficient. They express the
operation directly, without extra method calls. A function that uses default
operators is generic. It can be used with any type that supports the operation.

.. _s2.8.3-cons:
.. _283-cons:

.. _default-iterators-operators-cons:

2.8.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.8.3 Cons 

.. tab:: 中文

.. tab:: 英文

You can't tell the type of objects by reading the method names (unless the
variable has type annotations). This is also an advantage.

.. _s2.8.4-decision:
.. _284-decision:

.. _default-iterators-operators-decision:

2.8.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.8.4 Decision 

.. tab:: 中文

.. tab:: 英文

Use default iterators and operators for types that support them, like lists,
dictionaries, and files. The built-in types define iterator methods, too. Prefer
these methods to methods that return lists, except that you should not mutate a
container while iterating over it.

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

.. tab:: 英文

Use generators as needed.

.. _s2.9.1-definition:
.. _291-definition:

.. _generators-definition:

2.9.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.9.1 Definition 

.. tab:: 中文

.. tab:: 英文

A generator function returns an iterator that yields a value each time it
executes a yield statement. After it yields a value, the runtime state of the
generator function is suspended until the next value is needed.

.. _s2.9.2-pros:
.. _292-pros:

.. _generators-pros:

2.9.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.9.2 Pros 

.. tab:: 中文

.. tab:: 英文

Simpler code, because the state of local variables and control flow are
preserved for each call. A generator uses less memory than a function that
creates an entire list of values at once.

.. _s2.9.3-cons:
.. _293-cons:

.. _generators-cons:

2.9.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.9.3 Cons 

.. tab:: 中文

.. tab:: 英文

Local variables in the generator will not be garbage collected until the
generator is either consumed to exhaustion or itself garbage collected.

.. _s2.9.4-decision:
.. _294-decision:

.. _generators-decision:

2.9.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.9.4 Decision 

.. tab:: 中文

.. tab:: 英文

Fine. Use "Yields:" rather than "Returns:" in the docstring for generator
functions.

If the generator manages an expensive resource, make sure to force the clean up.

A good way to do the clean up is by wrapping the generator with a context
manager `PEP-0533 <https://peps.python.org/pep-0533/>`_ .

.. _s2.10-lambda-functions:
.. _210-lambda-functions:

.. _lambdas:

2.10 Lambda 函数
----------------------------

2.10 Lambda Functions 

.. tab:: 中文

.. tab:: 英文

Okay for one-liners. Prefer generator expressions over `map()` or `filter()`
with a `lambda`.

.. _s2.10.1-definition:
.. _2101-definition:

.. _lambdas-definition:

2.10.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.10.1 Definition 

.. tab:: 中文

.. tab:: 英文

Lambdas define anonymous functions in an expression, as opposed to a statement.

.. _s2.10.2-pros:
.. _2102-pros:

.. _lambdas-pros:

2.10.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.10.2 Pros 

.. tab:: 中文

.. tab:: 英文

Convenient.

.. _s2.10.3-cons:
.. _2103-cons:

.. _lambdas-cons:

2.10.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.10.3 Cons 

.. tab:: 中文

.. tab:: 英文

Harder to read and debug than local functions. The lack of names means stack
traces are more difficult to understand. Expressiveness is limited because the
function may only contain an expression.

.. _s2.10.4-decision:
.. _2104-decision:

.. _lambdas-decision:

2.10.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.10.4 Decision 

.. tab:: 中文

.. tab:: 英文

Lambdas are allowed. If the code inside the lambda function spans multiple lines
or is longer than 60-80 chars, it might be better to define it as a regular
`nested function <lexical-scoping_>`_.

For common operations like multiplication, use the functions from the :code:`operator`
module instead of lambda functions. For example, prefer :code:`operator.mul` to
:code:`lambda x, y: x * y`.

.. _s2.11-conditional-expressions:
.. _211-conditional-expressions:

.. _conditional-expressions:

2.11 条件表达式
----------------------------

2.11 Conditional Expressions 

.. tab:: 中文

.. tab:: 英文

Okay for simple cases.

.. _s2.11.1-definition:
.. _2111-definition:

.. _conditional-expressions-definition:

2.11.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.11.1 Definition 

.. tab:: 中文

.. tab:: 英文

Conditional expressions (sometimes called a “ternary operator”) are mechanisms
that provide a shorter syntax for if statements. For example: :code:`x = 1 if cond else 2`.

.. _s2.11.2-pros:
.. _2112-pros:

.. _conditional-expressions-pros:

2.11.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.11.2 Pros 

.. tab:: 中文

.. tab:: 英文

Shorter and more convenient than an if statement.

.. _s2.11.3-cons:
.. _2113-cons:

.. _conditional-expressions-cons:

2.11.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.11.3 Cons 

.. tab:: 中文

.. tab:: 英文

May be harder to read than an if statement. The condition may be difficult to
locate if the expression is long.

.. _s2.11.4-decision:
.. _2114-decision:

.. _conditional-expressions-decision:

2.11.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.11.4 Decision 

.. tab:: 中文

.. tab:: 英文

Okay to use for simple cases. Each portion must fit on one line:
true-expression, if-expression, else-expression. Use a complete if statement
when things get more complicated.

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

.. tab:: 英文

Okay in most cases.

.. _s2.12.1-definition:
.. _2121-definition:

.. _default-arguments-definition:

2.12.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.12.1 Definition 

.. tab:: 中文

.. tab:: 英文

You can specify values for variables at the end of a function's parameter list,
e.g., :code:`def foo(a, b=0):`. If :code:`foo` is called with only one argument, :code:`b` is set
to 0. If it is called with two arguments, :code:`b` has the value of the second
argument.

.. _s2.12.2-pros:
.. _2122-pros:

.. _default-arguments-pros:

2.12.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.12.2 Pros 

.. tab:: 中文

.. tab:: 英文

Often you have a function that uses lots of default values, but on rare
occasions you want to override the defaults. Default argument values provide an
easy way to do this, without having to define lots of functions for the rare
exceptions. As Python does not support overloaded methods/functions, default
arguments are an easy way of "faking" the overloading behavior.

.. _s2.12.3-cons:
.. _2123-cons:

.. _default-arguments-cons:

2.12.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.12.3 Cons 

.. tab:: 中文

.. tab:: 英文

Default arguments are evaluated once at module load time. This may cause
problems if the argument is a mutable object such as a list or a dictionary. If
the function modifies the object (e.g., by appending an item to a list), the
default value is modified.

.. _s2.12.4-decision:
.. _2124-decision:

.. _default-arguments-decision:

2.12.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.12.4 Decision 

.. tab:: 中文

.. tab:: 英文

Okay to use with the following caveat:

Do not use mutable objects as default values in the function or method
definition.

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

.. tab:: 英文

Properties may be used to control getting or setting attributes that require
trivial computations or logic. Property implementations must match the general
expectations of regular attribute access: that they are cheap, straightforward,
and unsurprising.

.. _s2.13.1-definition:
.. _2131-definition:

.. _properties-definition:

2.13.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.13.1 Definition 

.. tab:: 中文

.. tab:: 英文

A way to wrap method calls for getting and setting an attribute as a standard
attribute access.

.. _s2.13.2-pros:
.. _2132-pros:

.. _properties-pros:

2.13.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.13.2 Pros 

.. tab:: 中文

.. tab:: 英文

* Allows for an attribute access and assignment API rather than
  [getter and setter](#getters-and-setters) method calls.
* Can be used to make an attribute read-only.
* Allows calculations to be lazy.
* Provides a way to maintain the public interface of a class when the
  internals evolve independently of class users.

.. _s2.13.3-cons:
.. _2133-cons:

.. _properties-cons:

2.13.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.13.3 Cons 

.. tab:: 中文

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

.. tab:: 英文

Properties are allowed, but, like operator overloading, should only be used when
necessary and match the expectations of typical attribute access; follow the
[getters and setters](#getters-and-setters) rules otherwise.

For example, using a property to simply both get and set an internal attribute
isn't allowed: there is no computation occurring, so the property is unnecessary
([make the attribute public instead](#getters-and-setters)). In comparison,
using a property to control attribute access or to calculate a *trivially*
derived value is allowed: the logic is simple and unsurprising.

Properties should be created with the `@property`
[decorator](#s2.17-function-and-method-decorators). Manually implementing a
property descriptor is considered a [power feature](#power-features).

Inheritance with properties can be non-obvious. Do not use properties to
implement computations a subclass may ever want to override and extend.

.. _s2.14-truefalse-evaluations:
.. _214-truefalse-evaluations:

.. _truefalse-evaluations:

2.14 真/假判断
----------------------------

2.14 True/False Evaluations 

.. tab:: 中文

.. tab:: 英文

Use the "implicit" false if at all possible (with a few caveats).

.. _s2.14.1-definition:
.. _2141-definition:

.. _truefalse-evaluations-definition:

2.14.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.14.1 Definition 

.. tab:: 中文

.. tab:: 英文

Python evaluates certain values as :code:`False` when in a boolean context. A quick
"rule of thumb" is that all "empty" values are considered false, so :code:`0, None, [], {}, ''` all evaluate as false in a boolean context.

.. _s2.14.2-pros:
.. _2142-pros:

.. _truefalse-evaluations-pros:

2.14.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.14.2 Pros 

.. tab:: 中文

.. tab:: 英文

Conditions using Python booleans are easier to read and less error-prone. In
most cases, they're also faster.

.. _s2.14.3-cons:
.. _2143-cons:

.. _truefalse-evaluations-cons:

2.14.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.14.3 Cons 

.. tab:: 中文

.. tab:: 英文

May look strange to C/C++ developers.

.. _s2.14.4-decision:
.. _2144-decision:

.. _truefalse-evaluations-decision:

2.14.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.14.4 Decision 

.. tab:: 中文

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
    context. Prefer the :code:`.size` attribute when testing emptiness of a :code:`np.array`
    (e.g. :code:`if not users.size`).

.. _s2.16-lexical-scoping:
.. _216-lexical-scoping:

.. _lexical-scoping:

2.16 词法作用域
----------------------------

2.16 Lexical Scoping 

.. tab:: 中文

.. tab:: 英文

Okay to use.

.. _s2.16.1-definition:
.. _2161-definition:

.. _lexical-scoping-definition:

2.16.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.16.1 Definition 

.. tab:: 中文

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

.. tab:: 英文

Often results in clearer, more elegant code. Especially comforting to
experienced Lisp and Scheme (and Haskell and ML and ...) programmers.

.. _s2.16.3-cons:
.. _2163-cons:

.. _lexical-scoping-cons:

2.16.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.16.3 Cons 

.. tab:: 中文

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

.. tab:: 英文

Use decorators judiciously when there is a clear advantage. Avoid :code:`staticmethod` and limit use of :code:`classmethod`.

.. _s2.17.1-definition:
.. _2171-definition:

.. _decorators-definition:

2.17.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.17.1 Definition 

.. tab:: 中文

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

.. tab:: 英文

Elegantly specifies some transformation on a method; the transformation might eliminate some repetitive code, enforce invariants, etc.

.. _s2.17.3-cons:
.. _2173-cons:

.. _decorators-cons:

2.17.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.17.3 Cons 

.. tab:: 中文

.. tab:: 英文

Decorators can perform arbitrary operations on a function's arguments or return
values, resulting in surprising implicit behavior. Additionally, decorators
execute at object definition time. For module-level objects (classes, module
functions, ...) this happens at import time. Failures in decorator code are
pretty much impossible to recover from.

.. _s2.17.4-decision:
.. _2174-decision:

.. _decorators-decision:

2.17.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.17.4 Decision 

.. tab:: 中文

.. tab:: 英文

Use decorators judiciously when there is a clear advantage. Decorators should
follow the same import and naming guidelines as functions. A decorator docstring
should clearly state that the function is a decorator. Write unit tests for
decorators.

Avoid external dependencies in the decorator itself (e.g. don't rely on files,
sockets, database connections, etc.), since they might not be available when the
decorator runs (at import time, perhaps from :code:`pydoc` or other tools). A
decorator that is called with valid parameters should (as much as possible) be
guaranteed to succeed in all cases.

Decorators are a special case of "top-level code" - see [main](#s3.17-main) for
more discussion.

Never use :code:`staticmethod` unless forced to in order to integrate with an API
defined in an existing library. Write a module-level function instead.

Use :code:`classmethod` only when writing a named constructor, or a class-specific
routine that modifies necessary global state such as a process-wide cache.

.. _s2.18-threading:
.. _218-threading:

.. _threading:

2.18 线程
----------------------------

2.18 Threading 

.. tab:: 中文

.. tab:: 英文

Do not rely on the atomicity of built-in types.

While Python's built-in data types such as dictionaries appear to have atomic
operations, there are corner cases where they aren't atomic (e.g. if :code:`__hash__`
or :code:`__eq__` are implemented as Python methods) and their atomicity should not be
relied upon. Neither should you rely on atomic variable assignment (since this
in turn depends on dictionaries).

Use the :code:`queue` module's :code:`Queue` data type as the preferred way to communicate
data between threads. Otherwise, use the :code:`threading` module and its locking
primitives. Prefer condition variables and :code:`threading.Condition` instead of
using lower-level locks.

.. _s2.19-power-features:
.. _219-power-features:

.. _power-features:

2.19 强大功能
----------------------------

2.19 Power Features 

.. tab:: 中文

.. tab:: 英文

Avoid these features.

.. _s2.19.1-definition:
.. _2191-definition:

.. _power-features-definition:

2.19.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.19.1 Definition 

.. tab:: 中文

.. tab:: 英文

Python is an extremely flexible language and gives you many fancy features such
as custom metaclasses, access to bytecode, on-the-fly compilation, dynamic
inheritance, object reparenting, import hacks, reflection (e.g. some uses of
:code:`getattr()`), modification of system internals, :code:`__del__` methods implementing
customized cleanup, etc.

.. _s2.19.2-pros:
.. _2192-pros:

.. _power-features-pros:

2.19.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.19.2 Pros 

.. tab:: 中文

.. tab:: 英文

These are powerful language features. They can make your code more compact.

.. _s2.19.3-cons:
.. _2193-cons:

.. _power-features-cons:

2.19.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.19.3 Cons 

.. tab:: 中文

.. tab:: 英文

It's very tempting to use these "cool" features when they're not absolutely
necessary. It's harder to read, understand, and debug code that's using unusual
features underneath. It doesn't seem that way at first (to the original author),
but when revisiting the code, it tends to be more difficult than code that is
longer but is straightforward.

.. _s2.19.4-decision:
.. _2194-decision:

.. _power-features-decision:

2.19.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.19.4 Decision 

.. tab:: 中文

.. tab:: 英文

Avoid these features in your code.

Standard library modules and classes that internally use these features are okay
to use (for example, :code:`abc.ABCMeta`, :code:`dataclasses`, and :code:`enum`).

.. _s2.20-modern-python:
.. _220-modern-python:
.. _from-future-imports:

.. _modern-python:

2.20 现代 Python：from \_\_future\_\_ imports
--------------------------------------------------------

2.20 Modern Python: from \_\_future\_\_ imports 

.. tab:: 中文

.. tab:: 英文

New language version semantic changes may be gated behind a special future
import to enable them on a per-file basis within earlier runtimes.

.. _s2.20.1-definition:
.. _2201-definition:

.. _modern-python-definition:

2.20.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.20.1 Definition 

.. tab:: 中文

.. tab:: 英文

Being able to turn on some of the more modern features via :code:`from __future__ import` statements allows early use of features from expected future Python
versions.

.. _s2.20.2-pros:
.. _2202-pros:

.. _modern-python-pros:

2.20.2 优点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.20.2 Pros 

.. tab:: 中文

.. tab:: 英文

This has proven to make runtime version upgrades smoother as changes can be made
on a per-file basis while declaring compatibility and preventing regressions
within those files. Modern code is more maintainable as it is less likely to
accumulate technical debt that will be problematic during future runtime
upgrades.

.. _s2.20.3-cons:
.. _2203-cons:

.. _modern-python-cons:

2.20.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.20.3 Cons 

.. tab:: 中文

.. tab:: 英文

Such code may not work on very old interpreter versions prior to the
introduction of the needed future statement. The need for this is more common in
projects supporting an extremely wide variety of environments.

.. _s2.20.4-decision:
.. _2204-decision:

.. _modern-python-decision:

2.20.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.20.4 Decision 

.. tab:: 中文

.. tab:: 英文


from \_\_future\_\_ imports
""""""""""""""""""""""""""""""""""""

from \_\_future\_\_ imports

.. tab:: 中文

.. tab:: 英文



Use of :code:`from __future__ import` statements is encouraged. It allows a given
source file to start using more modern Python syntax features today. Once you no
longer need to run on a version where the features are hidden behind a
:code:`__future__` import, feel free to remove those lines.

In code that may execute on versions as old as 3.5 rather than >= 3.7, import:

.. code-block:: python
    
    from __future__ import generator_stop

For more information read the
`Python future statement definitions <https://docs.python.org/3/library/__future__.html>`_
documentation.

Please don't remove these imports until you are confident the code is only ever
used in a sufficiently modern environment. Even if you do not currently use the
feature a specific future import enables in your code today, keeping it in place
in the file prevents later modifications of the code from inadvertently
depending on the older behavior.

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

.. tab:: 英文

You can annotate Python code with
 `type hints <https://docs.python.org/3/library/typing.html>`_ . Type-check the code
at build time with a type checking tool like `pytype <https://github.com/google/pytype>`_ .
In most cases, when feasible, type annotations are in source files. For
third-party or extension modules, annotations can be in
`stub .pyi files <https://peps.python.org/pep-0484/#stub-filespytype>`_ .


.. _s2.21.1-definition:
.. _2211-definition:

.. _typed-code-definition:

2.21.1 定义
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.21.1 Definition 

.. tab:: 中文

.. tab:: 英文

Type annotations (or "type hints") are for function or method arguments and
return values:

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

.. tab:: 英文

Type annotations improve the readability and maintainability of your code. The
type checker will convert many runtime errors to build-time errors, and reduce
your ability to use [Power Features](#power-features).

.. _s2.21.3-cons:
.. _2213-cons:

.. _typed-code-cons:

2.21.3 缺点
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.21.3 Cons 

.. tab:: 中文

.. tab:: 英文

You will have to keep the type declarations up to date.
You might see type errors that you think are
valid code. Use of a
 `type checker <https://github.com/google/pytype>`_ 
may reduce your ability to use `Power Features <power-features_>`_ .

.. _s2.21.4-decision:
.. _2214-decision:

.. _typed-code-decision:

2.21.4 决策
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.21.4 Decision 

.. tab:: 中文

.. tab:: 英文

You are strongly encouraged to enable Python type analysis when updating code.
When adding or modifying public APIs, include type annotations and enable
checking via pytype in the build system. As static analysis is relatively new to
Python, we acknowledge that undesired side-effects (such as
wrongly
inferred types) may prevent adoption by some projects. In those situations,
authors are encouraged to add a comment with a TODO or link to a bug describing
the issue(s) currently preventing type annotation adoption in the BUILD file or
in the code itself as appropriate.