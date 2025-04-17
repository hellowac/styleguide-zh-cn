:orphan:

.. _s3-python-style-rules:
.. _3-python-style-rules:

.. _python-style-rules:

3 Python 代码风格规则
==========================

3 Python Style Rules 

.. tab:: 中文

.. tab:: 英文

.. _s3.1-semicolons:
.. _31-semicolons:

.. _semicolons:

3.1 分号
----------------------------

3.1 Semicolons 

.. tab:: 中文

    不要用分号结束行，也不要使用分号将两个语句放在同一行上。

.. tab:: 英文

    Do not terminate your lines with semicolons, and do not use semicolons to put two statements on the same line.

.. _s3.2-line-length:
.. _32-line-length:

.. _line-length:

3.2 行长
----------------------------

3.2 Line length 

.. tab:: 中文

    最大行宽限制为 *80 个字符*。
    
    以下情况是对 80 字符限制的明确例外:
    
    -   较长的 import 语句。
    -   注释中的 URL、路径名或较长的命令行标志。
    -   不包含空格、不便于换行的模块级长字符串常量，如 URL 或路径名。
        -   Pylint 的禁用注释（例如：:code:`# pylint: disable=invalid-name`）
    
    不要使用反斜杠进行 `显式换行 <https://docs.python.org/3/reference/lexical_analysis.html#explicit-line-joining>`_。
    
    应使用 Python 提供的 `括号、方括号或花括号内的隐式换行 <http://docs.python.org/reference/lexical_analysis.html#implicit-line-joining>`_。如有必要，可以为表达式增加一对额外的括号。
    
    请注意，这项规则并不禁止字符串中的反斜杠换行（见 :ref:`下文 <strings>` ）。
    
    .. code-block:: python
    
        正确: foo_bar(self, width, height, color='black', design=None, x='foo',
                       emphasis=None, highlight=0)
    
    .. code-block:: python
    
        正确: if (width == 0 and height == 0 and
                   color == 'red' and emphasis == 'strong'):
    
                 (bridge_questions.clarification_on
                  .average_airspeed_of.unladen_swallow) = 'African or European?'
    
                 with (
                     very_long_first_expression_function() as spam,
                     very_long_second_expression_function() as beans,
                     third_thing() as eggs,
                 ):
                   place_order(eggs, beans, spam, beans)
    
    .. code-block:: python
    
        错误: if width == 0 and height == 0 and \
                     color == 'red' and emphasis == 'strong':
    
                 bridge_questions.clarification_on \
                     .average_airspeed_of.unladen_swallow = 'African or European?'
    
                 with very_long_first_expression_function() as spam, \
                       very_long_second_expression_function() as beans, \
                       third_thing() as eggs:
                   place_order(eggs, beans, spam, beans)
    
    当字符串字面量无法容纳于一行时，使用括号实现隐式换行。
    
    .. code-block:: python
    
        x = ('This will build a very long long '
             'long long long long long long string')
    
    建议在尽可能高的语法层级进行换行。如果必须换两次行，建议在相同语法层级进行。
    
    .. code-block:: python
    
        正确: bridgekeeper.answer(
                     name="Arthur", quest=questlib.find(owner="Arthur", perilous=True))
    
                 answer = (a_long_line().of_chained_methods()
                           .that_eventually_provides().an_answer())
    
                 if (
                     config is None
                     or 'editor.language' not in config
                     or config['editor.language'].use_spaces is False
                 ):
                   use_tabs()
    
    .. code-block:: python
    
        错误: bridgekeeper.answer(name="Arthur", quest=questlib.find(
                    owner="Arthur", perilous=True))
    
                answer = a_long_line().of_chained_methods().that_eventually_provides(
                    ).an_answer()
    
                if (config is None or 'editor.language' not in config or config[
                    'editor.language'].use_spaces is False):
                  use_tabs()
    
    在注释中，如果有较长的 URL，可以将其单独放置在一行上。
    
    .. code-block:: python
    
        正确:  # See details at
               # http://www.example.com/us/developer/documentation/api/content/v2.0/csv_file_name_extension_full_specification.html
    
    .. code-block:: python
    
        错误:  # See details at
               # http://www.example.com/us/developer/documentation/api/content/v2.0/
               # csv_file_name_extension_full_specification.html
    
    请注意上述换行示例中的缩进风格；详见 :ref:`缩进 <s3.4-indentation>` 一节。
    
    :ref:`文档字符串 <docstrings>` 的摘要行必须控制在 80 个字符以内。
    
    对于其他所有超过 80 字符的情况，如果使用 `Black <https://github.com/psf/black>`_ 或 `Pyink <https://github.com/google/pyink>`_ 自动格式化工具仍无法将行缩短到限制之内，则允许超过最大长度。在合理的情况下，建议作者根据上述建议手动进行换行。

.. tab:: 英文

    Maximum line length is *80 characters*.
    
    Explicit exceptions to the 80 character limit:
    
    -   Long import statements.
    -   URLs, pathnames, or long flags in comments.
    -   Long string module-level constants not containing whitespace that would be
        inconvenient to split across lines such as URLs or pathnames.
        -   Pylint disable comments. (e.g.: :code:`# pylint: disable=invalid-name`)
    
    Do not use a backslash for `explicit line continuation <https://docs.python.org/3/reference/lexical_analysis.html#explicit-line-joining>`_ .
    
    Instead, make use of Python's `implicit line joining inside parentheses, brackets and braces <http://docs.python.org/reference/lexical_analysis.html#implicit-line-joining>`_ .
    If necessary, you can add an extra pair of parentheses around an expression.
    
    Note that this rule doesn't prohibit backslash-escaped newlines within strings
    (see :ref:`below <strings>` ).
    
    .. code-block:: python
    
        Yes: foo_bar(self, width, height, color='black', design=None, x='foo',
                     emphasis=None, highlight=0)
    
    .. code-block:: python
    
        Yes: if (width == 0 and height == 0 and
                 color == 'red' and emphasis == 'strong'):
        
             (bridge_questions.clarification_on
              .average_airspeed_of.unladen_swallow) = 'African or European?'
        
             with (
                 very_long_first_expression_function() as spam,
                 very_long_second_expression_function() as beans,
                 third_thing() as eggs,
             ):
               place_order(eggs, beans, spam, beans)
    
    .. code-block:: python
    
        No:  if width == 0 and height == 0 and \
                 color == 'red' and emphasis == 'strong':
        
             bridge_questions.clarification_on \
                 .average_airspeed_of.unladen_swallow = 'African or European?'
        
             with very_long_first_expression_function() as spam, \
                   very_long_second_expression_function() as beans, \
                   third_thing() as eggs:
               place_order(eggs, beans, spam, beans)
    
    When a literal string won't fit on a single line, use parentheses for implicit
    line joining.
    
    .. code-block:: python
    
        x = ('This will build a very long long '
             'long long long long long long string')
    
    Prefer to break lines at the highest possible syntactic level. If you must break
    a line twice, break it at the same syntactic level both times.
    
    .. code-block:: python
    
        Yes: bridgekeeper.answer(
                 name="Arthur", quest=questlib.find(owner="Arthur", perilous=True))
        
             answer = (a_long_line().of_chained_methods()
                       .that_eventually_provides().an_answer())
        
             if (
                 config is None
                 or 'editor.language' not in config
                 or config['editor.language'].use_spaces is False
             ):
               use_tabs()
        
    .. code-block:: python
    
        No: bridgekeeper.answer(name="Arthur", quest=questlib.find(
                owner="Arthur", perilous=True))
        
            answer = a_long_line().of_chained_methods().that_eventually_provides(
                ).an_answer()
        
            if (config is None or 'editor.language' not in config or config[
                'editor.language'].use_spaces is False):
              use_tabs()
    
    
    Within comments, put long URLs on their own line if necessary.
    
    .. code-block:: python
    
        Yes:  # See details at
              # http://www.example.com/us/developer/documentation/api/content/v2.0/csv_file_name_extension_full_specification.html
    
    .. code-block:: python
    
        No:  # See details at
             # http://www.example.com/us/developer/documentation/api/content/v2.0/
             #860csv_file_name_extension_full_specification.html
    
    Make note of the indentation of the elements in the line continuation examples
    above; see the :ref:`indentation <s3.4-indentation>` section for explanation.
    
    :ref:`Docstring <docstrings>` summary lines must remain within the 80 character
    limit.
    
    In all other cases where a line exceeds 80 characters, and the `Black <https://github.com/psf/black>`_ or `Pyink <https://github.com/google/pyink>`_ auto-formatter does not help bring the line below the limit, the line is allowed to exceed this maximum. Authors are encouraged to manually break the line up per the notes above when it is sensible.

.. _s3.3-parentheses:
.. _33-parentheses:

.. _parentheses:

3.3 括号
----------------------------

3.3 Parentheses 

.. tab:: 中文
    
    谨慎使用括号。
    
    对元组使用括号是可以的，但不是强制的。在 return 语句或条件语句中，除非用于隐式换行或用于构造元组，否则不要使用括号。
    
    .. code-block:: python
    
        正确: if foo:
                   bar()
               while x:
                   x = bar()
               if x and y:
                   bar()
               if not x:
                   bar()
               # 对于单元素元组，括号比逗号更易识别。
               onesie = (foo,)
               return foo
               return spam, beans
               return (spam, beans)
               for (x, y) in dict.items(): ...
    
    .. code-block:: python
    
        错误: if (x):
                   bar()
               if not(x):
                   bar()
               return (foo)

.. tab:: 英文

    Use parentheses sparingly.
    
    It is fine, though not required, to use parentheses around tuples. Do not use
    them in return statements or conditional statements unless using parentheses for
    implied line continuation or to indicate a tuple.
    
    .. code-block:: python
    
        Yes: if foo:
                 bar()
             while x:
                 x = bar()
             if x and y:
                 bar()
             if not x:
                 bar()
             # For a 1 item tuple the ()s are more visually obvious than the comma.
             onesie = (foo,)
             return foo
             return spam, beans
             return (spam, beans)
             for (x, y) in dict.items(): ...
    
    .. code-block:: python
    
        No:  if (x):
                 bar()
             if not(x):
                 bar()
             return (foo)

.. _s3.4-indentation:
.. _34-indentation:

.. _indentation:

3.4 缩进
----------------------------

3.4 Indentation 

.. tab:: 中文
    
    代码块缩进应为 *4 个空格*。
    
    严禁使用制表符（tab）。隐式换行应使被换行元素纵向对齐（参见 `行长示例 <s3.2-line-length_>`_），或采用 4 空格悬挂缩进。闭合括号（圆括号、方括号或花括号）可以放在表达式末尾，也可以单独占一行，但在后一种情况下，其缩进应与对应的开括号行保持一致。
    
    .. code-block:: python
    
        正确：  # 与起始定界符对齐
                foo = long_function_name(var_one, var_two,
                                         var_three, var_four)
                meal = (spam,
                        beans)
    
                # 字典中与起始定界符对齐
                foo = {
                    'long_dictionary_key': value1 +
                                           value2,
                    ...
                }
    
                # 4 空格悬挂缩进；首行无内容
                foo = long_function_name(
                    var_one, var_two, var_three,
                    var_four)
                meal = (
                    spam,
                    beans)
    
                # 4 空格悬挂缩进；首行无内容，闭括号单独成行
                foo = long_function_name(
                    var_one, var_two, var_three,
                    var_four
                )
                meal = (
                    spam,
                    beans,
                )
    
                # 字典中的 4 空格悬挂缩进
                foo = {
                    'long_dictionary_key':
                        long_dictionary_value,
                    ...
                }
    
    .. code-block:: python
    
        错误：  # 禁止首行包含内容
                foo = long_function_name(var_one, var_two,
                    var_three, var_four)
                meal = (spam,
                    beans)
    
                # 禁止使用 2 空格悬挂缩进
                foo = long_function_name(
                  var_one, var_two, var_three,
                  var_four)
    
                # 字典中不允许省略悬挂缩进
                foo = {
                    'long_dictionary_key':
                    long_dictionary_value,
                    ...
                }

.. tab:: 英文

    Indent your code blocks with *4 spaces*.
    
    Never use tabs. Implied line continuation should align wrapped elements
    vertically (see `line length examples <s3.2-line-length_>`_), or use a hanging
    4-space indent. Closing (round, square or curly) brackets can be placed at the
    end of the expression, or on separate lines, but then should be indented the
    same as the line with the corresponding opening bracket.
    
    .. code-block:: python
    
        Yes:   # Aligned with opening delimiter.
               foo = long_function_name(var_one, var_two,
                                        var_three, var_four)
               meal = (spam,
                       beans)
        
               # Aligned with opening delimiter in a dictionary.
               foo = {
                   'long_dictionary_key': value1 +
                                          value2,
                   ...
               }
        
               # 4-space hanging indent; nothing on first line.
               foo = long_function_name(
                   var_one, var_two, var_three,
                   var_four)
               meal = (
                   spam,
                   beans)
        
               # 4-space hanging indent; nothing on first line,
               # closing parenthesis on a new line.
               foo = long_function_name(
                   var_one, var_two, var_three,
                   var_four
               )
               meal = (
                   spam,
                   beans,
               )
        
               # 4-space hanging indent in a dictionary.
               foo = {
                   'long_dictionary_key':
                       long_dictionary_value,
                   ...
               }
    
    .. code-block:: python
    
        No:    # Stuff on first line forbidden.
               foo = long_function_name(var_one, var_two,
                   var_three, var_four)
               meal = (spam,
                   beans)
        
               # 2-space hanging indent forbidden.
               foo = long_function_name(
                 var_one, var_two, var_three,
                 var_four)
        
               # No hanging indent in a dictionary.
               foo = {
                   'long_dictionary_key':
                   long_dictionary_value,
                   ...
               }

.. _s3.4.1-trailing-comma:
.. _s3.4.1-trailing-commas:
.. _s3.4.1-trailing_comma:
.. _s3.4.1-trailing_commas:
.. _341-trailing_comma:
.. _341-trailing_commas:
.. _trailing_comma:
.. _trailing_commas:

.. _trailing-comma:

3.4.1 项序列中的尾随逗号？
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.4.1 Trailing commas in sequences of items? 

.. tab:: 中文
    
    推荐在元素序列中使用尾逗号，仅当关闭的容器标记 :code:`]` 、 :code:`)` 或 :code:`}` 不与最后一个元素出现在同一行时适用，同时也适用于只有一个元素的元组。尾逗号的存在也可作为提示，指示 Python 自动格式化工具 `Black <https://github.com/psf/black>`_ 或 `Pyink <https://github.com/google/pyink>`_ 将容器自动格式化为每行一个元素。

.. tab:: 英文

    Trailing commas in sequences of items are recommended only when the closing
    container token :code:`]`, :code:`)`, or :code:`}` does not appear on the same line as the final
    element, as well as for tuples with a single element. The presence of a trailing
    comma is also used as a hint to our Python code auto-formatter
    `Black <https://github.com/psf/black>`_ or  `Pyink <https://github.com/google/pyink>`_ 
    to direct it to auto-format the container of items to one item per line when the
    :code:`,` after the final element is present.

.. code-block:: python

    Yes:   golomb3 = [0, 1, 3]
           golomb4 = [
               0,
               1,
               4,
               6,
           ]

.. code-block:: python

    No:    golomb4 = [
               0,
               1,
               4,
               6,]
    
.. _s3.5-blank-lines:
.. _35-blank-lines:

.. _blank-lines:

3.5 空行
----------------------------

3.5 Blank Lines 

.. tab:: 中文
    
    顶层定义（函数或类定义）之间应留两个空行。方法定义之间，以及 :code:`class` 的文档字符串与第一个方法之间应留一个空行。在 :code:`def` 行之后不应添加空行。在函数或方法内部，可视情况使用单个空行进行分隔。
    
    空行不必紧贴定义。例如，紧邻函数、类或方法定义之前的相关注释是可以接受的。请考虑是否将注释合并进文档字符串中会更有帮助。

.. tab:: 英文

    Two blank lines between top-level definitions, be they function or class
    definitions. One blank line between method definitions and between the docstring
    of a :code:`class` and the first method. No blank line following a :code:`def` line. Use
    single blank lines as you judge appropriate within functions or methods.

    Blank lines need not be anchored to the definition. For example, related
    comments immediately preceding function, class, and method definitions can make
    sense. Consider if your comment might be more useful as part of the docstring.

.. _s3.6-whitespace:
.. _36-whitespace:

.. _whitespace:

3.6 空格
----------------------------

3.6 Whitespace 

.. tab:: 中文
    
    在标点符号周围使用空格时，应遵循标准排版规则。
    
    括号（圆括号、方括号、花括号）内部不应有空格。
    
    .. code-block:: python
    
        正确：spam(ham[1], {'eggs': 2}, [])
    
    .. code-block:: python
    
        错误：spam( ham[ 1 ], { 'eggs': 2 }, [ ] )
    
    逗号、分号或冒号前不应有空格。逗号、分号或冒号后应有一个空格，
    除非它出现在行尾。
    
    .. code-block:: python
    
        正确：if x == 4:
                 print(x, y)
             x, y = y, x
    
    .. code-block:: python
    
        错误：if x == 4 :
                 print(x , y)
             x , y = y , x
    
    调用函数、进行索引或切片操作时，起始括号前不应有空格。
    
    .. code-block:: python
    
        正确：spam(1)
    
    .. code-block:: python
    
        错误：spam (1)
    
    .. code-block:: python
    
        正确：dict['key'] = list[index]
    
    .. code-block:: python
    
        错误：dict ['key'] = list [index]
    
    禁止使用行尾空格。
    
    对于赋值（ :code:`=` ）、比较（ :code:`==, <, >, !=, <>, <=, >=, in, not in, is, is not`）以及布尔运算符（:code:`and, or, not`），应在二元运算符两边各加一个空格。对于算术运算符（ :code:`+` 、 :code:`-` 、 :code:`*` 、 :code:`/` 、 :code:`//` 、 :code:`%` 、 :code:`**` 、 :code:`@` ），是否加空格可根据实际判断。
    
    .. code-block:: python
    
        正确：x == 1
    
    .. code-block:: python
    
        错误：x<1
    
    传递关键字参数或定义默认参数值时，等号两边 **不应** 添加空格。
    **唯一的例外** 是：若带有类型注解（见 :ref:`typing-default-values`），则 **应** 在等号两边添加空格。
    
    .. code-block:: python
    
        正确：def complex(real, imag=0.0): return Magic(r=real, i=imag)
        正确：def complex(real, imag: float = 0.0): return Magic(r=real, i=imag)
    
    .. code-block:: python
    
        错误：def complex(real, imag = 0.0): return Magic(r = real, i = imag)
        错误：def complex(real, imag: float=0.0): return Magic(r = real, i = imag)
    
    不要使用空格对齐连续行上的符号（例如 :code:`:`、:code:`#`、:code:`=` 等），
    因为这会增加维护负担：
    
    .. code-block:: python
    
        正确：
            foo = 1000  # comment
            long_name = 2  # comment that should not be aligned
    
            dictionary = {
                'foo': 1,
                'long_name': 2,
            }
    
    .. code-block:: python
    
        错误：
            foo       = 1000  # comment
            long_name = 2     # comment that should not be aligned
    
            dictionary = {
                'foo'      : 1,
                'long_name': 2,
            }
    
.. tab:: 英文
    
    Follow standard typographic rules for the use of spaces around punctuation.
    
    No whitespace inside parentheses, brackets or braces.
    
    .. code-block:: python
    
        Yes: spam(ham[1], {'eggs': 2}, [])
    
    .. code-block:: python
    
        No:  spam( ham[ 1 ], { 'eggs': 2 }, [ ] )
    
    No whitespace before a comma, semicolon, or colon. Do use whitespace after a
    comma, semicolon, or colon, except at the end of the line.
    
    .. code-block:: python
    
        Yes: if x == 4:
                 print(x, y)
             x, y = y, x
    
    .. code-block:: python
    
        No:  if x == 4 :
                 print(x , y)
             x , y = y , x
    
    No whitespace before the open paren/bracket that starts an argument list,
    indexing or slicing.
    
    .. code-block:: python
    
        Yes: spam(1)
    
    .. code-block:: python
    
        No:  spam (1)
    
    .. code-block:: python
    
        Yes: dict['key'] = list[index]
    
    .. code-block:: python
    
        No:  dict ['key'] = list [index]
    
    No trailing whitespace.
    
    Surround binary operators with a single space on either side for assignment
    (:code:`=`), comparisons (:code:`==, <, >, !=, <>, <=, >=, in, not in, is, is not`), and
    Booleans (:code:`and, or, not`). Use your better judgment for the insertion of spaces
    around arithmetic operators (:code:`+`, :code:`-`, :code:`*`, :code:`/`, :code:`//`, :code:`%`, :code:`**`, :code:`@`).
    
    .. code-block:: python
        
        Yes: x == 1
    
    .. code-block:: python
        
        No:  x<1
    
    Never use spaces around `=` when passing keyword arguments or defining a default
    parameter value, with one exception:
    :ref:`when a type annotation is present <typing-default-values>`, *do* use spaces
    around the `=` for the default parameter value.
    
    .. code-block:: python
        
        Yes: def complex(real, imag=0.0): return Magic(r=real, i=imag)
        Yes: def complex(real, imag: float = 0.0): return Magic(r=real, i=imag)
    
    
    .. code-block:: python
        
        No:  def complex(real, imag = 0.0): return Magic(r = real, i = imag)
        No:  def complex(real, imag: float=0.0): return Magic(r = real, i = imag)
    
    
    Don't use spaces to vertically align tokens on consecutive lines, since it
    becomes a maintenance burden (applies to `:`, `#`, `=`, etc.):
    
    .. code-block:: python
    
        Yes:
            foo = 1000  # comment
            long_name = 2  # comment that should not be aligned
    
            dictionary = {
                'foo': 1,
                'long_name': 2,
            }
    
    .. code-block:: python
    
        No:
            foo       = 1000  # comment
            long_name = 2     # comment that should not be aligned
    
            dictionary = {
                'foo'      : 1,
                'long_name': 2,
            }


.. _Python_Interpreter:
.. _s3.7-shebang-line:
.. _37-shebang-line:

.. _shebang-line:

3.7 Shebang 行
----------------------------

3.7 Shebang Line 

.. tab:: 中文

    大多数 :code:`.py` 文件无需以 :code:`#!` 开头。程序的主文件应以如下之一开头：

    :code:`#!/usr/bin/env python3` （支持 virtualenv），或  
    :code:`#!/usr/bin/python3` （符合 `PEP-394 <https://peps.python.org/pep-0394/>`_ ）。

    此行用于内核查找 Python 解释器，但在模块被导入时会被 Python 忽略。
    它仅适用于打算直接执行的脚本文件。


.. tab:: 英文

    Most :code:`.py` files do not need to start with a :code:`#!` line. Start the main file of a
    program with :code:`#!/usr/bin/env python3` (to support virtualenvs) or :code:`#!/usr/bin/python3` per
    `PEP-394 <https://peps.python.org/pep-0394/>`_.

    This line is used by the kernel to find the Python interpreter, but is ignored by Python when importing modules. It is only necessary on a file intended to be executed directly.

.. _s3.8-comments-and-docstrings:
.. _s3.8-comments:
.. _38-comments-and-docstrings:

.. _documentation:

3.8 注释和文档字符串
----------------------------

3.8 Comments and Docstrings 

.. tab:: 中文

    确保对模块、函数、方法文档字符串和内联注释使用正确的样式。

.. tab:: 英文

    Be sure to use the right style for module, function, method docstrings and inline comments.

.. _s3.8.1-comments-in-doc-strings:
.. _381-docstrings:
.. _comments-in-doc-strings:

.. _docstrings:

3.8.1 文档字符串
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.8.1 Docstrings 

.. tab:: 中文

    Python 使用 *文档字符串* （docstring）来编写代码文档。文档字符串是包、模块、类或函数的首个语句（字符串）。这些字符串可通过对象的 :code:`__doc__` 成员自动提取，并被 :code:`pydoc` 使用。
    （试试运行 :code:`pydoc` 查看你的模块文档效果。）

    始终使用三重双引号 :code:`"""` 格式来书写文档字符串（参见
    `PEP 257 <https://peps.python.org/pep-0257/>`_）。文档字符串应以一行总结句开头（物理上是一行，不超过 80 个字符），并以句号、问号或感叹号结尾。

    若包含更多内容（鼓励这么做），应在总结句之后空一行，并从第一行引号所在位置开始继续书写剩余内容。

.. tab:: 英文

    Python uses *docstrings* to document code. A docstring is a string that is the
    first statement in a package, module, class or function. These strings can be
    extracted automatically through the :code:`__doc__` member of the object and are used
    by :code:`pydoc`.
    (Try running :code:`pydoc` on your module to see how it looks.) Always use the
    three-double-quote :code:`"""` format for docstrings (per
    `PEP 257 <https://peps.python.org/pep-0257/>`_ )). A docstring should be organized
    as a summary line (one physical line not exceeding 80 characters) terminated by
    a period, question mark, or exclamation point. When writing more (encouraged),
    this must be followed by a blank line, followed by the rest of the docstring
    starting at the same cursor position as the first quote of the first line. There
    are more formatting guidelines for docstrings below.

.. _s3.8.2-comments-in-modules:
.. _382-modules:
.. _comments-in-modules:

.. _module-docs:

3.8.2 模块
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.8.2 Modules 

.. tab:: 中文

    下面还会提供更多文档字符串的格式说明。

    每个文件都应包含许可协议的声明模板。根据项目使用的许可证选择合适的模板（如 Apache 2.0、BSD、LGPL、GPL 等）。

    文件开头应包含一个文档字符串，用于描述该模块的内容和用途。

    .. code-block:: python

        """该模块或程序的一行摘要，以句号结尾。

        留出一行空行。其余部分应包含对模块或程序的整体描述。
        可选地，还可以简要描述导出的类与函数，以及用法示例。

        常见使用示例：

        foo = ClassFoo()
        bar = foo.function_bar()
        """

.. tab:: 英文

    Every file should contain license boilerplate. Choose the appropriate boilerplate for the license used by the project (for example, Apache 2.0, BSD, LGPL, GPL).

    Files should start with a docstring describing the contents and usage of the
    module.

    .. code-block:: python

        """A one-line summary of the module or program, terminated by a period.

        Leave one blank line.  The rest of this docstring should contain an
        overall description of the module or program.  Optionally, it may also
        contain a brief description of exported classes and functions and/or usage
        examples.

        Typical usage example:

        foo = ClassFoo()
        bar = foo.function_bar()
        """


.. _s3.8.2.1-test-modules:

.. _test-docs:

3.8.2.1 测试模块
""""""""""""""""""""""""""""""""""""

3.8.2.1 Test modules 

.. tab:: 中文

    测试文件不要求必须具有模块级文档字符串。只有在可以提供额外信息的情况下才应添加。

    例如：测试的运行方式说明、非常规的初始化流程、对外部环境的依赖说明等。

    .. code-block:: python

        """该 blaze 测试使用 golden 文件。

        你可以通过运行如下命令来更新这些文件：
        `blaze run //foo/bar:foo_test -- --update_golden_files`
        （从 `google3` 目录中运行）。
        """

    如果文档字符串并未提供任何新信息，则不应写入。

    .. code-block:: python

        """Tests for foo.bar."""


.. tab:: 英文

    Module-level docstrings for test files are not required. They should be included
    only when there is additional information that can be provided.

    Examples include some specifics on how the test should be run, an explanation of
    an unusual setup pattern, dependency on the external environment, and so on.

    .. code-block:: python

        """This blaze test uses golden files.

        You can update those files by running
        `blaze run //foo/bar:foo_test -- --update_golden_files` from the `google3`
        directory.
        """


    Docstrings that do not provide any new information should not be used.

    .. code-block:: python

        """Tests for foo.bar."""


.. _s3.8.3-functions-and-methods:
.. _383-functions-and-methods:
.. _functions-and-methods:

.. _function-docs:

3.8.3 函数和方法
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.8.3 Functions and Methods 

.. tab:: 中文

    本节中，“函数”指的是方法、函数、生成器或属性。
    
    对于具备以下任一特征的函数， **必须** 编写文档字符串：
    
    -   是公共 API 的一部分
    -   体量较大
    -   逻辑不明显
    
    文档字符串应提供足够的信息，以便用户在无需查看函数实现的情况下，能够正确调用该函数。应描述函数的调用语法和语义， **通常不应** 包含实现细节，除非这些细节与函数的使用方式密切相关。例如，若函数会对其某个参数产生副作用，则应在文档中说明。否则，关于实现的细微但重要的细节应以代码注释的形式出现在实现中，而非文档字符串中。
    
    文档字符串可以使用描述式（如 :code:`"""Fetches rows from a Bigtable."""`）或祈使式（如 :code:`"""Fetch rows from a Bigtable."""`）的写法，但在同一个文件中应保持风格一致。对于 :code:`@property` 数据描述符，其文档风格应与属性或 `函数参数 <doc-function-args_>`_ 的文档风格一致（例如使用 :code:`"""The Bigtable path."""`，而非 :code:`"""Returns the Bigtable path."""`）。
    
    函数的文档字符串中某些内容应通过以下特殊小节进行描述。每个小节应以以冒号结尾的标题行开始。标题下方的内容应保持 2 或 4 个空格的悬挂缩进（文件内保持一致）。如果函数名称与签名已经足够清晰，可以用一行文档字符串简洁表达时，这些小节可以省略。
    
    .. _doc-function-args:
    
    :ref:`Args: <doc-function-args>`
        按名称列出每个参数，后接描述内容，两者之间用冒号加一个空格或换行分隔。
        若描述内容超过 80 字符一行，应使用比参数名缩进多 2 或 4 个空格的悬挂缩进（与文件中其他 docstring 保持一致）。若代码中未包含类型注解，则描述中应包含所需的类型信息。
        若函数接受 :code:`*foo` （可变长度参数）或 :code:`**bar` （任意关键字参数），应分别列为 :code:`*foo` 和 :code:`**bar`。
    
    .. _doc-function-returns:
    
    :ref:`Returns:（或 Yields:，用于生成器）<doc-function-returns>`
        描述返回值的语义，包括类型注解中未表达的信息。
        若函数仅返回 None，则可省略本节。若文档字符串以 “Return”, “Returns”, “Yield”, “Yields” 开头，且首句已充分描述返回值，也可省略此节，例如 :code:`"""Returns row from Bigtable as a tuple of strings."""`。
        不要模仿旧的 NumPy 风格（详见 `示例 <https://numpy.org/doc/1.24/reference/generated/numpy.linalg.qr.html>`_），即将返回的元组拆成多个返回值分别命名而不说明这是元组。应使用如下格式：
    
        ``Returns: A tuple (mat_a, mat_b), where mat_a is ..., and ...``
    
        文档中的辅助名称不一定与函数体中的变量名一致（这些变量名不属于 API 的一部分）。
        若函数使用了 :code:`yield`，则 :code:`Yields:` 部分应描述 :code:`next()` 返回的对象，而非该函数调用所返回的生成器对象。
    
    .. _doc-function-raises:
    
    :ref:`Raises: <doc-function-raises>`
        列出所有与接口相关的异常及其描述。
        使用与 *Args:* 部分相同的格式（异常名 + 冒号 + 空格或换行 + 悬挂缩进）。
        不应记录由于违反 docstring 中 API 规范而抛出的异常（因为这会使违例行为变成 API 的一部分，产生悖论）。
    
    .. code-block:: python
    
        def fetch_smalltable_rows(
            table_handle: smalltable.Table,
            keys: Sequence[bytes | str],
            require_all_keys: bool = False,
        ) -> Mapping[bytes, tuple[str, ...]]:
            """Fetches rows from a Smalltable.
    
            Retrieves rows pertaining to the given keys from the Table instance
            represented by table_handle.  String keys will be UTF-8 encoded.
    
            Args:
                table_handle: An open smalltable.Table instance.
                keys: A sequence of strings representing the key of each table
                  row to fetch.  String keys will be UTF-8 encoded.
                require_all_keys: If True only rows with values set for all keys will be
                  returned.
    
            Returns:
                A dict mapping keys to the corresponding table row data
                fetched. Each row is represented as a tuple of strings. For
                example:
    
                {b'Serak': ('Rigel VII', 'Preparer'),
                 b'Zim': ('Irk', 'Invader'),
                 b'Lrrr': ('Omicron Persei 8', 'Emperor')}
    
                Returned keys are always bytes.  If a key from the keys argument is
                missing from the dictionary, then that row was not found in the
                table (and require_all_keys must have been False).
    
            Raises:
                IOError: An error occurred accessing the smalltable.
            """
    
    也可以采用以下这种带换行的变体格式编写 :code:`Args:`：
    
    .. code-block:: python
    
        def fetch_smalltable_rows(
            table_handle: smalltable.Table,
            keys: Sequence[bytes | str],
            require_all_keys: bool = False,
        ) -> Mapping[bytes, tuple[str, ...]]:
            """Fetches rows from a Smalltable.
    
            Retrieves rows pertaining to the given keys from the Table instance
            represented by table_handle.  String keys will be UTF-8 encoded.
    
            Args:
              table_handle:
                An open smalltable.Table instance.
              keys:
                A sequence of strings representing the key of each table row to
                fetch.  String keys will be UTF-8 encoded.
              require_all_keys:
                If True only rows with values set for all keys will be returned.
    
            Returns:
              A dict mapping keys to the corresponding table row data
              fetched. Each row is represented as a tuple of strings. For
              example:
    
              {b'Serak': ('Rigel VII', 'Preparer'),
               b'Zim': ('Irk', 'Invader'),
               b'Lrrr': ('Omicron Persei 8', 'Emperor')}
    
              Returned keys are always bytes.  If a key from the keys argument is
              missing from the dictionary, then that row was not found in the
              table (and require_all_keys must have been False).
    
            Raises:
              IOError: An error occurred accessing the smalltable.
            """
    
.. tab:: 英文

    In this section, "function" means a method, function, generator, or property.
    
    A docstring is mandatory for every function that has one or more of the
    following properties:
    
    -   being part of the public API
    -   nontrivial size
    -   non-obvious logic
    
    A docstring should give enough information to write a call to the function
    without reading the function's code. The docstring should describe the
    function's calling syntax and its semantics, but generally not its
    implementation details, unless those details are relevant to how the function is
    to be used. For example, a function that mutates one of its arguments as a side
    effect should note that in its docstring. Otherwise, subtle but important
    details of a function's implementation that are not relevant to the caller are
    better expressed as comments alongside the code than within the function's
    docstring.
    
    The docstring may be descriptive-style (:code:`"""Fetches rows from a Bigtable."""`)
    or imperative-style (:code:`"""Fetch rows from a Bigtable."""`), but the style should
    be consistent within a file. The docstring for a :code:`@property` data descriptor
    should use the same style as the docstring for an attribute or a
    `function argument <doc-function-args_>`_ (:code:`"""The Bigtable path."""`,
    rather than :code:`"""Returns the Bigtable path."""`).
    
    Certain aspects of a function should be documented in special sections, listed
    below. Each section begins with a heading line, which ends with a colon. All
    sections other than the heading should maintain a hanging indent of two or four
    spaces (be consistent within a file). These sections can be omitted in cases
    where the function's name and signature are informative enough that it can be
    aptly described using a one-line docstring.
    
    `Args: <doc-function-args_>`_
        List each parameter by name. A description should follow the name, and be
        separated by a colon followed by either a space or newline. If the
        description is too long to fit on a single 80-character line, use a hanging
        indent of 2 or 4 spaces more than the parameter name (be consistent with the
        rest of the docstrings in the file). The description should include required
        type(s) if the code does not contain a corresponding type annotation. If a
        function accepts :code:`*foo` (variable length argument lists) and/or :code:`**bar`
        (arbitrary keyword arguments), they should be listed as :code:`*foo` and :code:`**bar`.
    
    `Returns: (or Yields: for generators) <doc-function-returns_>`_
        Describe the semantics of the return value, including any type information
        that the type annotation does not provide. If the function only returns
        None, this section is not required. It may also be omitted if the docstring
        starts with "Return", "Returns", "Yield", or "Yields" (e.g. :code:`"""Returns row from Bigtable as a tuple of strings."""`) *and* the opening sentence is
        sufficient to describe the return value. Do not imitate older 'NumPy style'
        (`example <https://numpy.org/doc/1.24/reference/generated/numpy.linalg.qr.html>`_),
        which frequently documented a tuple return value as if it were multiple
        return values with individual names (never mentioning the tuple). Instead,
        describe such a return value as: "Returns: A tuple (mat_a, mat_b), where
        mat_a is ..., and ...". The auxiliary names in the docstring need not
        necessarily correspond to any internal names used in the function body (as
        those are not part of the API). If the function uses :code:`yield` (is a
        generator), the :code:`Yields:` section should document the object returned by
        :code:`next()`, instead of the generator object itself that the call evaluates to.
    
    `Raises: <doc-function-raises_>`_
        List all exceptions that are relevant to the interface followed by a
        description. Use a similar exception name + colon + space or newline and
        hanging indent style as described in *Args:*. You should not document
        exceptions that get raised if the API specified in the docstring is violated
        (because this would paradoxically make behavior under violation of the API
        part of the API).
    
    .. code-block:: python
    
        def fetch_smalltable_rows(
            table_handle: smalltable.Table,
            keys: Sequence[bytes | str],
            require_all_keys: bool = False,
        ) -> Mapping[bytes, tuple[str, ...]]:
            """Fetches rows from a Smalltable.
        
            Retrieves rows pertaining to the given keys from the Table instance
            represented by table_handle.  String keys will be UTF-8 encoded.
        
            Args:
                table_handle: An open smalltable.Table instance.
                keys: A sequence of strings representing the key of each table
                  row to fetch.  String keys will be UTF-8 encoded.
                require_all_keys: If True only rows with values set for all keys will be
                  returned.
        
            Returns:
                A dict mapping keys to the corresponding table row data
                fetched. Each row is represented as a tuple of strings. For
                example:
        
                {b'Serak': ('Rigel VII', 'Preparer'),
                 b'Zim': ('Irk', 'Invader'),
                 b'Lrrr': ('Omicron Persei 8', 'Emperor')}
        
                Returned keys are always bytes.  If a key from the keys argument is
                missing from the dictionary, then that row was not found in the
                table (and require_all_keys must have been False).
        
            Raises:
                IOError: An error occurred accessing the smalltable.
            """
    
    Similarly, this variation on :code:`Args:` with a line break is also allowed:
    
    .. code-block:: python
    
        def fetch_smalltable_rows(
            table_handle: smalltable.Table,
            keys: Sequence[bytes | str],
            require_all_keys: bool = False,
        ) -> Mapping[bytes, tuple[str, ...]]:
            """Fetches rows from a Smalltable.
        
            Retrieves rows pertaining to the given keys from the Table instance
            represented by table_handle.  String keys will be UTF-8 encoded.
        
            Args:
              table_handle:
                An open smalltable.Table instance.
              keys:
                A sequence of strings representing the key of each table row to
                fetch.  String keys will be UTF-8 encoded.
              require_all_keys:
                If True only rows with values set for all keys will be returned.
        
            Returns:
              A dict mapping keys to the corresponding table row data
              fetched. Each row is represented as a tuple of strings. For
              example:
        
              {b'Serak': ('Rigel VII', 'Preparer'),
               b'Zim': ('Irk', 'Invader'),
               b'Lrrr': ('Omicron Persei 8', 'Emperor')}
        
              Returned keys are always bytes.  If a key from the keys argument is
              missing from the dictionary, then that row was not found in the
              table (and require_all_keys must have been False).
        
            Raises:
              IOError: An error occurred accessing the smalltable.
            """
    
.. _s3.8.3.1-overridden-methods:

.. _overridden-method-docs:

3.8.3.1 重写方法
""""""""""""""""""""""""""""""""""""

3.8.3.1 Overridden Methods 

.. tab:: 中文

    如果一个方法重写了基类的方法，并且显式使用了 `@override <https://typing-extensions.readthedocs.io/en/latest/#override>`_ 装饰器（来自 :code:`typing_extensions` 或 :code:`typing` 模块），则 **不需要** 为该方法编写文档字符串，除非重写方法在语义上对基类方法的契约进行了重要改进，或需要提供额外细节（例如记录额外的副作用）。此时，应在重写的方法中撰写包含这些差异的文档字符串。

    .. code-block:: python

        from typing_extensions import override

        class Parent:
            def do_something(self):
                """Parent method, includes docstring."""

        # 子类中使用 @override 注解的方法
        class Child(Parent):
            @override
            def do_something(self):
                pass

    .. code-block:: python

        # 子类中未使用 @override 装饰器，此时必须提供文档字符串
        class Child(Parent):
            def do_something(self):
                pass

        # 文档字符串内容可非常简略；@override 已表明基类中有文档
        class Child(Parent):
            @override
            def do_something(self):
                """See base class."""

.. tab:: 英文

    A method that overrides a method from a base class does not need a docstring if
    it is explicitly decorated with
    `@override <https://typing-extensions.readthedocs.io/en/latest/#override>`_
    (from :code:`typing_extensions` or :code:`typing` modules), unless the overriding method's
    behavior materially refines the base method's contract, or details need to be
    provided (e.g., documenting additional side effects), in which case a docstring
    with at least those differences is required on the overriding method.

    .. code-block:: python

        from typing_extensions import override

        class Parent:
            def do_something(self):
                """Parent method, includes docstring."""

        # Child class, method annotated with override.
        class Child(Parent):
            @override
            def do_something(self):
                pass

    .. code-block:: python

        # Child class, but without @override decorator, a docstring is required.
        class Child(Parent):
            def do_something(self):
                pass

        # Docstring is trivial, @override is sufficient to indicate that docs can be
        # found in the base class.
        class Child(Parent):
            @override
            def do_something(self):
                """See base class."""

.. _s3.8.4-comments-in-classes:
.. _384-classes:
.. _comments-in-classes:

.. _class-docs:

3.8.4 类
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.8.4 Classes 

.. tab:: 中文

    类定义下方应提供类的文档字符串，对类本身进行说明。公共属性（不包括 :ref:`properties <properties>` ）应在文档字符串中的 :code:`Attributes` 小节中记录，格式应与 :ref:`函数参数 <doc-function-args>` 的格式一致。

    .. code-block:: python

        class SampleClass:
            """此类的简要说明。

            更详细的类信息...
            更详细的类信息...

            Attributes:
                likes_spam: 一个布尔值，表示我们是否喜欢 SPAM。
                eggs: 我们产下的鸡蛋数量。
            """

            def __init__(self, likes_spam: bool = False):
                """根据 SPAM 喜好初始化实例。

                Args:
                    likes_spam: 指示实例是否具有此偏好。
                """
                self.likes_spam = likes_spam
                self.eggs = 0

            @property
            def butter_sticks(self) -> int:
                """我们拥有的黄油棒数量。"""

    所有类的文档字符串应以一行简短摘要开始，描述类实例的含义。也就是说，继承自 :code:`Exception` 的子类也应说明该异常的代表意义，而非其可能出现的上下文。类的文档字符串不应重复无谓信息，例如“这个类是一个类”。

    .. code-block:: python

        # 推荐写法：
        class CheeseShopAddress:
            """奶酪商店的地址。

            ...
            """

        class OutOfCheeseError(Exception):
            """没有奶酪可用了。"""

    .. code-block:: python

        # 不推荐写法：
        class CheeseShopAddress:
            """描述奶酪商店地址的类。

            ...
            """

        class OutOfCheeseError(Exception):
            """当没有奶酪可用时抛出。"""

.. tab:: 英文

    Classes should have a docstring below the class definition describing the class.
    Public attributes, excluding `properties <properties_>`_ , should be documented
    here in an :code:`Attributes` section and follow the same formatting as a
    `function's Args <doc-function-args_>`_ section.

    .. code-block:: python

        class SampleClass:
            """Summary of class here.

            Longer class information...
            Longer class information...

            Attributes:
                likes_spam: A boolean indicating if we like SPAM or not.
                eggs: An integer count of the eggs we have laid.
            """

            def __init__(self, likes_spam: bool = False):
                """Initializes the instance based on spam preference.

                Args:
                likes_spam: Defines if instance exhibits this preference.
                """
                self.likes_spam = likes_spam
                self.eggs = 0

            @property
            def butter_sticks(self) -> int:
                """The number of butter sticks we have."""

    All class docstrings should start with a one-line summary that describes what
    the class instance represents. This implies that subclasses of :code:`Exception`
    should also describe what the exception represents, and not the context in which
    it might occur. The class docstring should not repeat unnecessary information,
    such as that the class is a class.

    .. code-block:: python

        # Yes:
        class CheeseShopAddress:
            """The address of a cheese shop.

            ...
            """

        class OutOfCheeseError(Exception):
            """No more cheese is available."""

    .. code-block:: python

        # No:
        class CheeseShopAddress:
            """Class that describes the address of a cheese shop.

            ...
            """

        class OutOfCheeseError(Exception):
            """Raised when no more cheese is available."""

.. _s3.8.5-block-and-inline-comments:
.. _comments-in-block-and-inline:
.. _s3.8.5-comments-in-block-and-inline:
.. _385-block-and-inline-comments:

.. _comments:

3.8.5 块注释和内联注释
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.8.5 Block and Inline Comments 

.. tab:: 中文

    代码中最后一种注释的位置是出现在逻辑复杂的部分。如果你觉得下一次在 `代码审查 <http://en.wikipedia.org/wiki/Code_review>`_ 中需要解释它，那就现在写注释。复杂操作前应加几行注释说明；而不明显的操作可以在行尾加注释。

    .. code-block:: python

        # 我们使用加权字典搜索来确定 i 在数组中的位置。
        # 我们根据数组中最大值和数组长度推测其位置，
        # 然后使用二分查找确定精确位置。

        if i & (i-1) == 0:  # 若 i 为 0 或 2 的幂，此条件为 True。

    为了提升可读性，这类注释应距代码至少两个空格，用 :code:`#` 起始，并在其后留至少一个空格再写注释内容。

    另一方面， **永远不要注释代码本身的语法逻辑**。假设阅读你代码的人比你更懂 Python，但不一定理解你在做什么。

    .. code-block:: python

        # 不良注释示例：遍历 b 数组，确保每次出现 i 后面紧跟的是 i+1

.. tab:: 英文

    The final place to have comments is in tricky parts of the code. If you're going
    to have to explain it at the next  `code review <http://en.wikipedia.org/wiki/Code_review>`_ ,
    you should comment it now. Complicated operations get a few lines of comments
    before the operations commence. Non-obvious ones get comments at the end of the
    line.

    .. code-block:: python

        # We use a weighted dictionary search to find out where i is in
        # the array.  We extrapolate position based on the largest num
        # in the array and the array size and then do binary search to
        # get the exact number.

        if i & (i-1) == 0:  # True if i is 0 or a power of 2.


    To improve legibility, these comments should start at least 2 spaces away from
    the code with the comment character :code:`#`, followed by at least one space before
    the text of the comment itself.

    On the other hand, never describe the code. Assume the person reading the code
    knows Python (though not what you're trying to do) better than you do.

    .. code-block:: python

        # BAD COMMENT: Now go through the b array and make sure whenever i occurs
        # the next element is i+1


.. The next section is copied from the C++ style guide. 

.. _s3.8.6-punctuation-spelling-and-grammar:
.. _386-punctuation-spelling-and-grammar:
.. _spelling:
.. _punctuation:
.. _grammar:

.. _punctuation-spelling-grammar:

3.8.6 标点符号、拼写和语法
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.8.6 Punctuation, Spelling, and Grammar 

.. tab:: 中文

    注意标点、拼写和语法；良好撰写的注释比糟糕的注释更容易阅读。
    
    注释应当像叙述性文本一样可读，使用正确的大小写和标点。在许多情况下，完整的句子比句子片段更易于理解。简短的注释（例如出现在代码行末的注释）可以稍微不那么正式，但你应在风格上保持一致。
    
    尽管有时可能会因为审阅者指出你用了逗号而不是分号而感到沮丧，但维护源码的清晰性和可读性至关重要。正确的标点、拼写和语法有助于实现这一目标。

.. tab:: 英文

    Pay attention to punctuation, spelling, and grammar; it is easier to read
    well-written comments than badly written ones.

    Comments should be as readable as narrative text, with proper capitalization and
    punctuation. In many cases, complete sentences are more readable than sentence
    fragments. Shorter comments, such as comments at the end of a line of code, can
    sometimes be less formal, but you should be consistent with your style.

    Although it can be frustrating to have a code reviewer point out that you are
    using a comma when you should be using a semicolon, it is very important that
    source code maintain a high level of clarity and readability. Proper
    punctuation, spelling, and grammar help with that goal.

.. _s3.10-strings:
.. _310-strings:

.. _strings:

3.10 字符串
----------------------------

3.10 Strings 

.. tab:: 中文
    
    即使参数全是字符串，也请使用
    `f-string <https://docs.python.org/3/reference/lexical_analysis.html#f-strings>`_、
    :code:`%` 运算符，或 :code:`format` 方法来格式化字符串。请根据实际判断选择合适的字符串格式化方式。使用单个 :code:`+` 拼接是可以接受的，但不要用 :code:`+` 进行格式化。
    
    .. code-block:: python
    
        Yes: x = f'name: {name}; score: {n}'
             x = '%s, %s!' % (imperative, expletive)
             x = '{}, {}'.format(first, second)
             x = 'name: %s; score: %d' % (name, n)
             x = 'name: %(name)s; score: %(score)d' % {'name':name, 'score':n}
             x = 'name: {}; score: {}'.format(name, n)
             x = a + b
    
    .. code-block:: python
    
        No: x = first + ', ' + second
            x = 'name: ' + name + '; score: ' + str(n)
    
    避免在循环中使用 :code:`+` 或 :code:`+=` 来累加字符串。在某些情况下，使用加法来累加字符串会导致运行时间从线性退化为二次方。虽然 CPython 在某些常见场景中会对这种模式进行优化，但那只是实现细节。优化何时生效难以预测，且可能发生变化。相反，应该将每个子字符串添加到列表中，并在循环结束后使用 :code:`''.join` 拼接，或写入 :code:`io.StringIO` 缓冲区。这些技术能始终保持摊销线性时间复杂度。
    
    .. code-block:: python
    
        Yes: items = ['<table>']
             for last_name, first_name in employee_list:
                 items.append('<tr><td>%s, %s</td></tr>' % (last_name, first_name))
             items.append('</table>')
             employee_table = ''.join(items)
    
    .. code-block:: python
    
        No: employee_table = '<table>'
            for last_name, first_name in employee_list:
                employee_table += '<tr><td>%s, %s</td></tr>' % (last_name, first_name)
            employee_table += '</table>'
    
    在同一个文件中，字符串的引号类型应保持一致。选择 `'` 或 `"` 其一，并统一使用。为避免字符串中引号字符需要转义，可以使用另一种类型的引号。
    
    .. code-block:: python
    
        Yes:
            Python('Why are you hiding your eyes?')
            Gollum("I'm scared of lint errors.")
            Narrator('"Good!" thought a happy Python reviewer.')
    
    .. code-block:: python
    
        No:
            Python("Why are you hiding your eyes?")
            Gollum('The lint. It burns. It burns us.')
            Gollum("Always the great lint. Watching. Watching.")
    
    多行字符串推荐使用 :code:`"""`，而不是 :code:`'''`。如果某个项目统一使用 :code:`'` 作为普通字符串的引号，也可以统一使用 :code:`'''` 作为非文档字符串的多行字符串引号。但无论何种情况，文档字符串必须使用 :code:`"""`。
    
    多行字符串不会随程序其余部分缩进对齐。如果需要避免字符串中嵌入多余空格，可以使用连接的单行字符串，或者配合
    `textwrap.dedent() <https://docs.python.org/3/library/textwrap.html#textwrap.dedent>`_
    来移除每行前部的统一空格。
    
    .. code-block:: python
    
        No:
          long_string = """This is pretty ugly.
        Don't do this.
        """
    
    .. code-block:: python
    
        Yes:
        long_string = """This is fine if your use case can accept
            extraneous leading spaces."""
    
    .. code-block:: python
    
        Yes:
        long_string = ("And this is fine if you cannot accept\n" +
                       "extraneous leading spaces.")
    
    .. code-block:: python
      
        Yes:
        long_string = ("And this too is fine if you cannot accept\n"
                       "extraneous leading spaces.")
    
    .. code-block:: python
      
        Yes:
        import textwrap
      
        long_string = textwrap.dedent("""\
            This is also fine, because textwrap.dedent()
            will collapse common leading spaces in each line.""")
    
    请注意，这里的反斜杠并不违反
    `禁止显式换行续行 <line-length_>`_ 的规则；在这种情况下，反斜杠是用于
    `转义换行符 <https://docs.python.org/3/reference/lexical_analysis.html#string-and-bytes-literals>`_ 的。

.. tab:: 英文

    Use an
    `f-string <https://docs.python.org/3/reference/lexical_analysis.html#f-strings>`_,
    the :code:`%` operator, or the :code:`format` method for formatting strings, even when the
    parameters are all strings. Use your best judgment to decide between string
    formatting options. A single join with :code:`+` is okay but do not format with :code:`+`.
    
    .. code-block:: python
    
        Yes: x = f'name: {name}; score: {n}'
             x = '%s, %s!' % (imperative, expletive)
             x = '{}, {}'.format(first, second)
             x = 'name: %s; score: %d' % (name, n)
             x = 'name: %(name)s; score: %(score)d' % {'name':name, 'score':n}
             x = 'name: {}; score: {}'.format(name, n)
             x = a + b
    
    .. code-block:: python
    
        No: x = first + ', ' + second
            x = 'name: ' + name + '; score: ' + str(n)
    
    Avoid using the :code:`+` and :code:`+=` operators to accumulate a string within a loop. In
    some conditions, accumulating a string with addition can lead to quadratic
    rather than linear running time. Although common accumulations of this sort may
    be optimized on CPython, that is an implementation detail. The conditions under
    which an optimization applies are not easy to predict and may change. Instead,
    add each substring to a list and :code:`''.join` the list after the loop terminates,
    or write each substring to an :code:`io.StringIO` buffer. These techniques
    consistently have amortized-linear run-time complexity.
    
    .. code-block:: python
    
        Yes: items = ['<table>']
             for last_name, first_name in employee_list:
                 items.append('<tr><td>%s, %s</td></tr>' % (last_name, first_name))
             items.append('</table>')
             employee_table = ''.join(items)
    
    .. code-block:: python
    
        No: employee_table = '<table>'
            for last_name, first_name in employee_list:
                employee_table += '<tr><td>%s, %s</td></tr>' % (last_name, first_name)
            employee_table += '</table>'
    
    Be consistent with your choice of string quote character within a file. Pick :code:`'`
    or :code:`"` and stick with it. It is okay to use the other quote character on a
    string to avoid the need to backslash-escape quote characters within the string.
    
    .. code-block:: python
    
        Yes:
            Python('Why are you hiding your eyes?')
            Gollum("I'm scared of lint errors.")
            Narrator('"Good!" thought a happy Python reviewer.')
    
    .. code-block:: python
    
        No:
            Python("Why are you hiding your eyes?")
            Gollum('The lint. It burns. It burns us.')
            Gollum("Always the great lint. Watching. Watching.")
    
    Prefer :code:`"""` for multi-line strings rather than :code:`'''`. Projects may choose to
    use :code:`'''` for all non-docstring multi-line strings if and only if they also use
    :code:`'` for regular strings. Docstrings must use :code:`"""` regardless.
    
    Multi-line strings do not flow with the indentation of the rest of the program.
    If you need to avoid embedding extra space in the string, use either
    concatenated single-line strings or a multi-line string with
    `textwrap.dedent() <https://docs.python.org/3/library/textwrap.html#textwrap.dedent>`_
    to remove the initial space on each line:
    
    .. code-block:: python
    
        No:
          long_string = """This is pretty ugly.
        Don't do this.
        """
    
    
    .. code-block:: python
    
        Yes:
        long_string = """This is fine if your use case can accept
            extraneous leading spaces."""
    
    .. code-block:: python
    
        Yes:
        long_string = ("And this is fine if you cannot accept\n" +
                       "extraneous leading spaces.")
    
    .. code-block:: python
      
        Yes:
        long_string = ("And this too is fine if you cannot accept\n"
                       "extraneous leading spaces.")
    
    .. code-block:: python
      
        Yes:
        import textwrap
      
        long_string = textwrap.dedent("""\
            This is also fine, because textwrap.dedent()
            will collapse common leading spaces in each line.""")
    
    Note that using a backslash here does not violate the prohibition against
    `explicit line continuation <line-length_>`_; in this case, the backslash is
    `escaping a newline <https://docs.python.org/3/reference/lexical_analysis.html#string-and-bytes-literals>`_
    in a string literal.
    
.. _s3.10.1-logging:
.. _3101-logging:
.. _logging:

.. _logging:

3.10.1 日志记录
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.10.1 Logging 

.. tab:: 中文
    
    对于那些第一个参数为模式字符串（包含 :code:`%` 占位符）的日志函数：始终使用字符串字面量（ **不要使用 f-string！** ）作为第一个参数，并将格式化参数作为后续参数传入。一些日志系统会收集未展开的模式字符串作为可查询字段。此外，这种方式还可避免在没有任何日志器配置为输出该信息时，浪费时间去渲染日志内容。
    
    .. code-block:: python
    
        Yes:
        import tensorflow as tf
        logger = tf.get_logger()
        logger.info('TensorFlow Version is: %s', tf.__version__)
    
    .. code-block:: python
    
        Yes:
        import os
        from absl import logging
    
        logging.info('Current $PAGER is: %s', os.getenv('PAGER', default=''))
    
        homedir = os.getenv('HOME')
        if homedir is None or not os.access(homedir, os.W_OK):
                logging.error('Cannot write to home directory, $HOME=%r', homedir)
    
    .. code-block:: python
    
        No:
        import os
        from absl import logging
    
        logging.info('Current $PAGER is:')
        logging.info(os.getenv('PAGER', default=''))
    
        homedir = os.getenv('HOME')
        if homedir is None or not os.access(homedir, os.W_OK):
            logging.error(f'Cannot write to home directory, $HOME={homedir!r}')

.. tab:: 英文

    For logging functions that expect a pattern-string (with %-placeholders) as
    their first argument: Always call them with a string literal (not an f-string!)
    as their first argument with pattern-parameters as subsequent arguments. Some
    logging implementations collect the unexpanded pattern-string as a queryable
    field. It also prevents spending time rendering a message that no logger is
    configured to output.

    .. code-block:: python

        Yes:
        import tensorflow as tf
        logger = tf.get_logger()
        logger.info('TensorFlow Version is: %s', tf.__version__)

    .. code-block:: python

        Yes:
        import os
        from absl import logging

        logging.info('Current $PAGER is: %s', os.getenv('PAGER', default=''))

        homedir = os.getenv('HOME')
        if homedir is None or not os.access(homedir, os.W_OK):
                logging.error('Cannot write to home directory, $HOME=%r', homedir)

    .. code-block:: python

        No:
        import os
        from absl import logging

        logging.info('Current $PAGER is:')
        logging.info(os.getenv('PAGER', default=''))

        homedir = os.getenv('HOME')
        if homedir is None or not os.access(homedir, os.W_OK):
            logging.error(f'Cannot write to home directory, $HOME={homedir!r}')

.. _s3.10.2-error-messages:
.. _3102-error-messages:
.. _error-messages:

.. _error-messages:

3.10.2 错误消息
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.10.2 Error Messages 

.. tab:: 中文
    
    错误消息（例如 :code:`ValueError` 异常的信息字符串，或展示给用户的消息）应遵循以下三条原则：
    
    1. 消息应准确描述实际的错误条件。
    2. 被插入的内容应始终清晰可识别。
    3. 应便于自动化处理（例如使用 grep 工具搜索）。
    
    .. code-block:: python
    
        Yes:
        if not 0 <= p <= 1:
            raise ValueError(f'Not a probability: {p=}')
    
        try:
            os.rmdir(workdir)
        except OSError as error:
            logging.warning('Could not remove directory (reason: %r): %r',
                            error, workdir)
    
    .. code-block:: python
    
        No:
        if p < 0 or p > 1:  # 问题：float('nan') 时该条件也为 False！
            raise ValueError(f'Not a probability: {p=}')
    
        try:
            os.rmdir(workdir)
        except OSError:
            # 问题：该信息作出了未必正确的假设：
            # 删除失败可能还有其他原因，可能误导调试者。
            logging.warning('Directory already was deleted: %s', workdir)
    
        try:
            os.rmdir(workdir)
        except OSError:
            # 问题：该消息不易被 grep 等工具搜索，
            # 且对于某些 `workdir` 值也容易产生歧义。
            # 假设某人传入了 workdir = 'deleted'，那么警告内容会是：
            # “The deleted directory could not be deleted.”
            logging.warning('The %s directory could not be deleted.', workdir)

.. tab:: 英文

    Error messages (such as: message strings on exceptions like :code:`ValueError`, or
    messages shown to the user) should follow three guidelines:

    1. The message needs to precisely match the actual error condition.
    2. Interpolated pieces need to always be clearly identifiable as such.
    3. They should allow simple automated processing (e.g. grepping).

    .. code-block:: python

        Yes:
        if not 0 <= p <= 1:
            raise ValueError(f'Not a probability: {p=}')

        try:
            os.rmdir(workdir)
        except OSError as error:
            logging.warning('Could not remove directory (reason: %r): %r',
                            error, workdir)

    .. code-block:: python

        No:
        if p < 0 or p > 1:  # PROBLEM: also false for float('nan')!
            raise ValueError(f'Not a probability: {p=}')

        try:
            os.rmdir(workdir)
        except OSError:
            # PROBLEM: Message makes an assumption that might not be true:
            # Deletion might have failed for some other reason, misleading
            # whoever has to debug this.
            logging.warning('Directory already was deleted: %s', workdir)

        try:
            os.rmdir(workdir)
        except OSError:
            # PROBLEM: The message is harder to grep for than necessary, and
            # not universally non-confusing for all possible values of `workdir`.
            # Imagine someone calling a library function with such code
            # using a name such as workdir = 'deleted'. The warning would read:
            # "The deleted directory could not be deleted."
            logging.warning('The %s directory could not be deleted.', workdir)

.. _s3.11-files-sockets-closeables:
.. _s3.11-files-and-sockets:
.. _311-files-and-sockets:
.. _files-and-sockets:

.. _files:

3.11 文件、套接字和类似的有状态资源
-------------------------------------------------------------

3.11 Files, Sockets, and similar Stateful Resources 

.. tab:: 中文
    
    在完成文件和套接字操作后应显式关闭它们。这条规则自然地也适用于那些内部使用套接字的可关闭资源（如数据库连接），以及其他需要类似关闭方式的资源。例如：
    
    - `mmap <https://docs.python.org/3/library/mmap.html>`_ 映射对象，
    - `h5py 文件对象 <https://docs.h5py.org/en/stable/high/file.html>`_，
    - `matplotlib.pyplot 图形窗口 <https://matplotlib.org/2.1.0/api/_as_gen/matplotlib.pyplot.close.html>`_ 等。
    
    不必要地保持文件、套接字或其他有状态对象处于打开状态，会带来许多负面影响：
    
    - 它们可能会消耗有限的系统资源（如文件描述符）。如果代码涉及大量此类对象，在未及时释放的情况下可能会耗尽系统资源。
    - 保持文件处于打开状态，可能阻止移动、删除文件，或卸载文件系统。
    - 程序中共享的文件或套接字，在逻辑上已关闭后可能仍被读取或写入。如果这些对象确实已被关闭，再访问它们会抛出异常，从而尽早暴露问题。
    
    此外，虽然文件和套接字（以及其他类似资源）在对象被销毁时通常会自动关闭，但将对象的生命周期与资源状态耦合是个不良实践：
    
    - 无法保证运行时会在何时调用 :code:`__del__` 方法。不同的 Python 实现使用不同的内存管理机制（如延迟垃圾回收），可能会使对象生命周期任意延长。
    - 出现在全局变量或异常回溯中的意外引用，可能使对象存活时间超出预期。
    
    历史经验不断重申：依赖析构器（finalizer）来自动清理那些具有可观察副作用的资源，会带来严重问题，跨越多个编程语言和几十年的实践（参考：
    `这篇关于 Java 的文章 <https://wiki.sei.cmu.edu/confluence/display/java/MET12-J.+Do+not+use+finalizers>`_）。
    
    推荐的资源管理方式是使用
    `with 语句 <http://docs.python.org/reference/compound_stmts.html#the-with-statement>`_：
    
    .. code-block:: python
    
        with open("hello.txt") as hello_file:
            for line in hello_file:
                print(line)
    
    对于不支持 :code:`with` 语句的类似文件对象，可使用 :code:`contextlib.closing()`：
    
    .. code-block:: python
    
        import contextlib
    
        with contextlib.closing(urllib.urlopen("http://www.python.org/")) as front_page:
            for line in front_page:
                print(line)
    
    在极少数无法使用上下文管理的情况下，必须在代码文档中清楚说明资源的生命周期管理方式。

.. tab:: 英文

    Explicitly close files and sockets when done with them. This rule naturally
    extends to closeable resources that internally use sockets, such as database
    connections, and also other resources that need to be closed down in a similar
    fashion. To name only a few examples, this also includes
    `mmap <https://docs.python.org/3/library/mmap.html>`_ mappings,
    `h5py File objects <https://docs.h5py.org/en/stable/high/file.html>`_, and
    `matplotlib.pyplot figure windows <https://matplotlib.org/2.1.0/api/_as_gen/matplotlib.pyplot.close.html>`_.
    
    Leaving files, sockets or other such stateful objects open unnecessarily has
    many downsides:
    
    - They may consume limited system resources, such as file descriptors. Code
      that deals with many such objects may exhaust those resources unnecessarily
      if they're not returned to the system promptly after use.
    - Holding files open may prevent other actions such as moving or deleting
      them, or unmounting a filesystem.
    - Files and sockets that are shared throughout a program may inadvertently be
      read from or written to after logically being closed. If they are actually
      closed, attempts to read or write from them will raise exceptions, making
      the problem known sooner.
    
    Furthermore, while files and sockets (and some similarly behaving resources) are
    automatically closed when the object is destructed, coupling the lifetime of the
    object to the state of the resource is poor practice:
    
    - There are no guarantees as to when the runtime will actually invoke the
      :code:`__del__` method. Different Python implementations use different memory
      management techniques, such as delayed garbage collection, which may
      increase the object's lifetime arbitrarily and indefinitely.
    - Unexpected references to the file, e.g. in globals or exception tracebacks,
      may keep it around longer than intended.
    
    Relying on finalizers to do automatic cleanup that has observable side effects
    has been rediscovered over and over again to lead to major problems, across many
    decades and multiple languages (see e.g.
    `this article <https://wiki.sei.cmu.edu/confluence/display/java/MET12-J.+Do+not+use+finalizers>`_
    for Java).
    
    The preferred way to manage files and similar resources is using the
    `with statement <http://docs.python.org/reference/compound_stmts.html#the-with-statement>`_:
    
    .. code-block:: python
    
        with open("hello.txt") as hello_file:
            for line in hello_file:
                print(line)
    
    For file-like objects that do not support the :code:`with` statement, use :code:`contextlib.closing()`:
    
    .. code-block:: python
    
        import contextlib
    
        with contextlib.closing(urllib.urlopen("http://www.python.org/")) as front_page:
            for line in front_page:
                print(line)
    
    In rare cases where context-based resource management is infeasible, code
    documentation must explain clearly how resource lifetime is managed.

.. _s3.12-todo-comments:
.. _312-todo-comments:

.. _todo:

3.12 TODO 注释
----------------------------

3.12 TODO Comments 

.. tab:: 中文

    使用 :code:`TODO` 注释来标记临时代码、短期解决方案，或目前“够用但不完美”的实现。

    一个标准的 :code:`TODO` 注释应以全大写的单词 :code:`TODO` 开头，后跟一个冒号，然后附带一个用于提供上下文的链接， **理想情况下是一个 bug 跟踪链接**。推荐使用 bug 链接是因为这些问题通常会被追踪，并附带后续的讨论信息。在链接之后，应添加一个由连字符 :code:`-` 引出的解释性描述。

    这样做的目的是统一 :code:`TODO` 的格式，以便后续可以通过搜索统一样式找到更多上下文细节。

    .. code-block:: python

        # TODO: crbug.com/192795 - Investigate cpufreq optimizations.

    旧的注释样式（过去推荐，但不建议在新代码中使用）如下：

    .. code-block:: python

        # TODO(crbug.com/192795): Investigate cpufreq optimizations.
        # TODO(yourusername): Use a "\*" here for concatenation operator.

    避免添加将上下文归因于某个人或团队的 :code:`TODO` 注释：

    .. code-block:: python

        # TODO: @yourusername - File an issue and use a '*' for repetition.

    如果你的 :code:`TODO` 是类似“将来某个时间点进行某事”的形式，请确保包含 **非常明确的日期** （例如 “Fix by November 2009”）或 **非常明确的事件** （例如 “Remove this code when all clients can handle XML responses.”），这样将来的维护者才能理解其时机。最好还是通过 issue 跟踪这些任务。

.. tab:: 英文

    Use :code:`TODO` comments for code that is temporary, a short-term solution, or
    good-enough but not perfect.

    A :code:`TODO` comment begins with the word :code:`TODO` in all caps, a following colon, and
    a link to a resource that contains the context, ideally a bug reference. A bug
    reference is preferable because bugs are tracked and have follow-up comments.
    Follow this piece of context with an explanatory string introduced with a hyphen
    :code:`-`. 
    The purpose is to have a consistent :code:`TODO` format that can be searched to find
    out how to get more details. 

    .. code-block:: python

        # TODO: crbug.com/192795 - Investigate cpufreq optimizations.


    Old style, formerly recommended, but discouraged for use in new code:


    .. code-block:: python
    
        # TODO(crbug.com/192795): Investigate cpufreq optimizations.
        # TODO(yourusername): Use a "\*" here for concatenation operator.

    Avoid adding TODOs that refer to an individual or team as the context:

    .. code-block:: python
        
        # TODO: @yourusername - File an issue and use a '*' for repetition.

    If your :code:`TODO` is of the form "At a future date do something" make sure that you
    either include a very specific date ("Fix by November 2009") or a very specific
    event ("Remove this code when all clients can handle XML responses.") that
    future code maintainers will comprehend. Issues are ideal for tracking this.

.. _s3.13-imports-formatting:
.. _313-imports-formatting:

.. _imports-formatting:

3.13 导入格式
--------------------------------

3.13 Imports formatting 

.. tab:: 中文

    导入语句应使用 **单独的行**；不过对于 `typing` 和 `collections.abc` 中的类型导入，有例外（详见 `<typing-imports_>`_）。

    例如：

    .. code-block:: python

        Yes: from collections.abc import Mapping, Sequence
            import os
            import sys
            from typing import Any, NewType

    .. code-block:: python

        No:  import os, sys

    所有导入语句都应放在文件顶部，即模块注释与文档字符串之后，模块的全局变量和常量之前。导入语句应按照“越通用越靠前”的顺序进行分组：

    1. **Python 的 future 导入语句。** 例如：

       .. code-block:: python

           from __future__ import annotations

       详情见上文的 :ref:`from-future-imports` 。

    2. **Python 标准库导入。** 例如：

       .. code-block:: python

            import sys

    3. **第三方模块或包导入。** （来自 PyPI，例如）：

       .. code-block:: python

            import tensorflow as tf

    4. **代码库中的子包导入。** 例如：

       .. code-block:: python

            from otherproject.ai import mind

    5. **（已废弃）** 与当前文件位于同一顶级子包中的应用专属导入。例如：

       .. code-block:: python

            from myproject.backend.hgwells import time_machine

       你可能会在一些较旧的 Google Python Style 代码中见到这种导入风格，但这已不再是推荐做法。**新代码建议不要刻意区分**，直接将应用特定的子包导入当作普通子包导入即可。

    在每个导入分组内，导入语句应按模块完整路径（即 :code:`from path import ...` 中的 path） **不区分大小写地按字典序排序**。可以在各导入分组之间添加空行（可选）。

    .. code-block:: python

        import collections
        import queue
        import sys

        from absl import app
        from absl import flags
        import bs4
        import cryptography
        import tensorflow as tf

        from book.genres import scifi
        from myproject.backend import huxley
        from myproject.backend.hgwells import time_machine
        from myproject.backend.state_machine import main_loop
        from otherproject.ai import body
        from otherproject.ai import mind
        from otherproject.ai import soul

        # 旧风格代码可能将这些导入放在下方：
        #from myproject.backend.hgwells import time_machine
        #from myproject.backend.state_machine import main_loop

.. tab:: 英文

    Imports should be on separate lines; there are
    `exceptions for typing and collections.abc imports <typing-imports_>`_.

    E.g.:

    .. code-block:: python

        Yes: from collections.abc import Mapping, Sequence
            import os
            import sys
            from typing import Any, NewType

    .. code-block:: python

        No:  import os, sys


    Imports are always put at the top of the file, just after any module comments
    and docstrings and before module globals and constants. Imports should be
    grouped from most generic to least generic:

    1.  Python future import statements. For example:

        .. code-block:: python
        
            from __future__ import annotations

        See `above <from-future-imports_>`_ for more information about those.

    2.  Python standard library imports. For example:

        .. code-block:: python
            
            import sys

    3.  `third-party <https://pypi.org/>`_  module or package imports. For example:

        
        .. code-block:: python
        
            import tensorflow as tf

    4.  Code repository sub-package imports. For example:

        
        .. code-block:: python
        
            from otherproject.ai import mind

    5.  **Deprecated:** application-specific imports that are part of the same top-level
        sub-package as this file. For example:

        
        .. code-block:: python
        
            from myproject.backend.hgwells import time_machine

        You may find older Google Python Style code doing this, but it is no longer
        required. **New code is encouraged not to bother with this.** Simply treat
        application-specific sub-package imports the same as other sub-package
        imports.

        
    Within each grouping, imports should be sorted lexicographically, ignoring case,
    according to each module's full package path (the :code:`path` in :code:`from path import ...`). Code may optionally place a blank line between import sections.

    .. code-block:: python

        import collections
        import queue
        import sys

        from absl import app
        from absl import flags
        import bs4
        import cryptography
        import tensorflow as tf

        from book.genres import scifi
        from myproject.backend import huxley
        from myproject.backend.hgwells import time_machine
        from myproject.backend.state_machine import main_loop
        from otherproject.ai import body
        from otherproject.ai import mind
        from otherproject.ai import soul

        # Older style code may have these imports down here instead:
        #from myproject.backend.hgwells import time_machine
        #from myproject.backend.state_machine import main_loop


.. _s3.14-statements:
.. _314-statements:

.. _statements:

3.14 语句
--------------------------------

3.14 Statements 

.. tab:: 中文

    通常每行只能写一个语句。

    但是，只有当整个语句可以放在一行时，才可以将测试结果与测试放在同一行。特别是，您永远不能对 :code:`try`/:code:`except` 这样做，因为 :code:`try` 和 :code:`except` 不能同时放在同一行；并且，只有在没有 :code:`else` 的情况下，您才能对 :code:`if` 这样做。

.. tab:: 英文

    Generally only one statement per line.

    However, you may put the result of a test on the same line as the test only if the entire statement fits on one line. In particular, you can never do so with :code:`try`/:code:`except` since the :code:`try` and :code:`except` can't both fit on the same line, and you can only do so with an :code:`if` if there is no :code:`else`.

.. code-block:: python

    Yes:

    if foo: bar(foo)

.. code-block:: python
    
    No:

    if foo: bar(foo)
    else:   baz(foo)

    try:               bar(foo)
    except ValueError: baz(foo)

    try:
        bar(foo)
    except ValueError: baz(foo)

.. _s3.15-accessors:
.. _s3.15-access-control:
.. _315-access-control:
.. _access-control:
.. _accessors:

.. _getters-and-setters:

3.15 Getter 和 Setter
--------------------------------

3.15 Getters and Setters 

.. tab:: 中文

    Getter 和 setter 函数（也称为访问器和修改器）应在它们用于获取或设置变量值时具备实际含义或行为时使用。

    特别是，当获取或设置某个变量的过程很复杂，或开销很大（无论是当前还是在合理预期的将来）时，应使用 getter/setter 函数。

    例如，如果一对 getter/setter 只是单纯地读取和写入一个内部属性，那么这个属性应直接设为公有。相比之下，如果设置某个变量会使某些状态失效或需要重建，那就应该使用 setter 函数。函数调用的形式表明此操作 **可能** 不是一个轻量的赋值。或者，如果只涉及简单逻辑，也可以使用 :ref:`属性 <properties>`，或通过重构来避免使用 getter/setter。

    Getter 和 setter 应遵循 :ref:`命名规范 <s3.16-naming>`，例如使用 :code:`get_foo()` 和 :code:`set_foo()`。

    如果旧代码是通过属性访问变量的，不要将新的 getter/setter 函数绑定到该属性。**任何仍试图使用旧方法访问该变量的代码都应抛出错误，以便让开发者意识到该访问现在更复杂。**

.. tab:: 英文

    Getter and setter functions (also called accessors and mutators) should be used
    when they provide a meaningful role or behavior for getting or setting a
    variable's value.

    In particular, they should be used when getting or setting the variable is
    complex or the cost is significant, either currently or in a reasonable future.

    If, for example, a pair of getters/setters simply read and write an internal
    attribute, the internal attribute should be made public instead. By comparison,
    if setting a variable means some state is invalidated or rebuilt, it should be a
    setter function. The function invocation hints that a potentially non-trivial
    operation is occurring. Alternatively, :ref:`properties <properties>` may be an
    option when simple logic is needed, or refactoring to no longer need getters and
    setters.

    Getters and setters should follow the :ref:`Naming <s3.16-naming>` guidelines, such
    as :code:`get_foo()` and :code:`set_foo()`.

    If the past behavior allowed access through a property, do not bind the new
    getter/setter functions to the property. Any code still attempting to access the
    variable by the old method should break visibly so they are made aware of the
    change in complexity.

.. _s3.16-naming:
.. _316-naming:

.. _naming:

3.16 命名
--------------------------------

3.16 Naming 

.. tab:: 中文

    :code:`module_name`, :code:`package_name`, :code:`ClassName`, :code:`method_name`, :code:`ExceptionName`,
    :code:`function_name`, :code:`GLOBAL_CONSTANT_NAME`, :code:`global_var_name`, :code:`instance_var_name`,
    :code:`function_parameter_name`, :code:`local_var_name`, :code:`query_proper_noun_for_thing`,
    :code:`send_acronym_via_https`.

    命名应具备描述性。这包括函数、类、变量、属性、文件名及所有其他具名实体。

    避免使用缩写。尤其是，避免使用歧义缩写或项目外读者不熟悉的缩写，也不要通过省略词中间的字母来构造缩写。

    文件应始终使用 :code:`.py` 扩展名，**永远不要使用连字符（-）**。

.. tab:: 英文


    Names should be descriptive. This includes functions, classes, variables,
    attributes, files and any other type of named entities.

    Avoid abbreviation. In particular, do not use abbreviations that are ambiguous
    or unfamiliar to readers outside your project, and do not abbreviate by deleting
    letters within a word.

    Always use a :code:`.py` filename extension. Never use dashes.

.. _s3.16.1-names-to-avoid:
.. _3161-names-to-avoid:

.. _names-to-avoid:

3.16.1 应避免的名称
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.16.1 Names to Avoid 

.. tab:: 中文

    不推荐的命名包括：
    
    - 单字符名称，除非在以下特定场景中使用：
    
      - 用作计数器或迭代器（如 :code:`i`, :code:`j`, :code:`k`, :code:`v` 等）
      - 在 :code:`try/except` 语句中作为异常标识符的 :code:`e`
      - 在 :code:`with` 语句中作为文件句柄的 :code:`f`
      - 无约束的私有 :ref:`类型变量 <typing-type-var>` （例如 :code:`_T = TypeVar("_T")`, :code:`_P = ParamSpec("_P")`）
      - 与参考论文或算法中的既有符号一致的名称（详见 :ref:`数学符号规范 <math-notation>` ）
    
      请注意不要滥用单字符名称。一般而言，命名的描述性应与其 **可见范围的大小成正比** 。例如，在一个 5 行代码块中使用 :code:`i` 可能是可以接受的，但在多层嵌套作用域中则显得过于模糊。
    
    - 包或模块名中使用连字符（:code:`-`）
    
    - 使用 Python 保留的 :code:`__双下划线开头并结尾__` 的名称
    
    - 使用攻击性术语
    
    - 包含变量类型却无实际意义的名称（例如 :code:`id_to_name_dict`）

.. tab:: 英文

    -   single character names, except for specifically allowed cases:

        -   counters or iterators (e.g. :code:`i`, :code:`j`, :code:`k`, :code:`v`, et al.)
        -   :code:`e` as an exception identifier in :code:`try/except` statements.
        -   :code:`f` as a file handle in :code:`with` statements
        -   private :ref:`type variables <typing-type-var>` with no constraints (e.g.
            :code:`_T = TypeVar("_T")`, :code:`_P = ParamSpec("_P")`)
        -   names that match established notation in a reference paper or algorithm
            (see :ref:`Mathematical Notation <math-notation>` )

        Please be mindful not to abuse single-character naming. Generally speaking,
        descriptiveness should be proportional to the name's scope of visibility.
        For example, :code:`i` might be a fine name for 5-line code block but within
        multiple nested scopes, it is likely too vague.

    -   dashes (:code:`-`) in any package/module name

    -   :code:`__double_leading_and_trailing_underscore__` names (reserved by Python)

    -   offensive terms

    -   names that needlessly include the type of the variable (for example:
        :code:`id_to_name_dict`)

.. _s3.16.2-naming-conventions:
.. _3162-naming-convention:

.. _naming-conventions:

3.16.2 命名约定
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.16.2 Naming Conventions 

.. tab:: 中文

    -   "Internal" 是指模块内部，或者类中的受保护或私有成员。
    
    -   在模块变量和函数名前添加单个下划线 (:code:`_`) 有助于保护它们（静态分析工具会标记访问受保护成员的行为）。请注意，单元测试可以访问被测试模块中的受保护常量。
    
    -   在实例变量或方法名前添加双下划线 (:code:`__`，即 "dunder") 会有效地将该变量或方法设为类的私有成员（通过名称重整）。我们不推荐使用双下划线，因为它会影响可读性和可测试性，且它并不是真正的私有。建议使用单下划线。
    
    -   将相关的类和顶层函数放在同一个模块中。与 Java 不同，Python 中没有必要将每个模块限制为仅包含一个类。
    
    -   使用 CapWords 风格为类命名，但为模块命名时使用 `lower_with_under.py` 风格。虽然一些旧模块使用 CapWords 命名（如 `CapWords.py`），但这已经不推荐使用，因为当模块名称与类名相同时容易产生混淆。比如："等一下，我是写了 :code:`import StringIO` 还是 :code:`from StringIO import StringIO`？"
    
    -   新的 *单元测试* 文件遵循 PEP 8 的 `lower_with_under` 方法命名风格，例如： :code:`test_<method_under_test>_<state>`。为了与遵循 CapWords 函数命名的旧模块保持一致，单元测试中的方法名称可以通过在 `test` 开头添加下划线来分隔逻辑组件。一个可能的命名模式是： :code:`test<MethodUnderTest>_<state>`。

.. tab:: 英文

    -   "Internal" means internal to a module, or protected or private within a
        class.

    -   Prepending a single underscore (:code:`_`) has some support for protecting module
        variables and functions (linters will flag protected member access). Note
        that it is okay for unit tests to access protected constants from the
        modules under test.

    -   Prepending a double underscore (:code:`__` aka "dunder") to an instance variable
        or method effectively makes the variable or method private to its class
        (using name mangling); we discourage its use as it impacts readability and
        testability, and isn't *really* private. Prefer a single underscore.

    -   Place related classes and top-level functions together in a
        module.
        Unlike Java, there is no need to limit yourself to one class per module.

    -   Use CapWords for class names, but lower_with_under.py for module names.
        Although there are some old modules named CapWords.py, this is now
        discouraged because it's confusing when the module happens to be named after
        a class. ("wait -- did I write :code:`import StringIO` or :code:`from StringIO import StringIO`?")

    -   New *unit test* files follow PEP 8 compliant lower_with_under method
        names, for example, :code:`test_<method_under_test>_<state>`. For consistency(\*)
        with legacy modules that follow CapWords function names, underscores may
        appear in method names starting with :code:`test` to separate logical components
        of the name. One possible pattern is :code:`test<MethodUnderTest>_<state>`.

.. _s3.16.3-file-naming:
.. _3163-file-naming:

.. _file-naming:

3.16.3 文件命名
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.16.3 File Naming 

.. tab:: 中文

    Python 文件名必须以 :code:`.py` 为扩展名，且不能包含短划线 (:code:`-`)。这样才能导入和单元测试这些文件名。如果您希望可执行文件无需扩展名即可访问，请使用符号链接或包含 :code:`exec "$0.py" "$@"` 的简单 bash 包装器。

.. tab:: 英文

    Python filenames must have a :code:`.py` extension and must not contain dashes (:code:`-`). This allows them to be imported and unittested. If you want an executable to be accessible without the extension, use a symbolic link or a simple bash wrapper containing :code:`exec "$0.py" "$@"`.

.. _s3.16.4-guidelines-derived-from-guidos-recommendations:
.. _3164-guidelines-derived-from-guidos-recommendations:

.. _guidelines-derived-from-guidos-recommendations:

3.16.4 源自 `Guido <https://en.wikipedia.org/wiki/Guido_van_Rossum>`_ 建议的指南
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.16.4 Guidelines derived from `Guido <https://en.wikipedia.org/wiki/Guido_van_Rossum>`_ 's Recommendations 

.. tab:: 中文

.. tab:: 英文

.. csv-table:: 
   :header: "Type", "Public", "Internal"

   "Packages", :code:`lower_with_under`,
   "Modules", :code:`lower_with_under`	:code:`_lower_with_under`
   "Classes", :code:`CapWords`, :code:`_CapWords`
   "Exceptions", :code:`CapWords`,
   "Functions", :code:`lower_with_under()`, :code:`_lower_with_under()`
   "Global/Class Constants", :code:`CAPS_WITH_UNDER`, :code:`_CAPS_WITH_UNDER`
   "Global/Class Variables", :code:`lower_with_under`, :code:`_lower_with_under`
   "Instance Variables", :code:`lower_with_under`, :code:`_lower_with_under (protected)`
   "Method Names", :code:`lower_with_under()`, :code:`_lower_with_under() (protected)`
   "Function/Method Parameters", :code:`lower_with_under`,
   "Local Variables", :code:`lower_with_under`,


.. _s3.17-main:
.. _317-main:

.. _math-notation:

3.16.5 数学符号
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.16.5 Mathematical Notation 

.. tab:: 中文

    对于涉及大量数学运算的代码，当变量名符合参考论文或算法中的约定符号时，即使这些短名称违反了样式指南，也是可以接受的。

    当使用基于既定符号的名称时：

    1. 在注释或文档字符串中引用所有命名约定的来源，最好附上学术资源的超链接。如果来源不可访问，则清楚地记录命名约定。
    2. 对于公共 API，优先使用符合 PEP8 的 :code:`descriptive_names`，因为它们更有可能在上下文之外遇到。
    3. 使用局部作用域的 :code:`pylint: disable=invalid-name` 指令来关闭警告。对于少数几个变量，可以将该指令作为行尾注释；对于更多变量，则可以在代码块开始处应用该指令。

.. tab:: 英文

    For mathematically-heavy code, short variable names that would otherwise violate
    the style guide are preferred when they match established notation in a
    reference paper or algorithm.

    When using names based on established notation:

    1. Cite the source of all naming conventions, preferably with a hyperlink to
    academic resource itself, in a comment or docstring. If the source is not
    accessible, clearly document the naming conventions.
    2. Prefer PEP8-compliant :code:`descriptive_names` for public APIs, which are much
    more likely to be encountered out of context.
    3. Use a narrowly-scoped :code:`pylint: disable=invalid-name` directive to silence
    warnings. For just a few variables, use the directive as an endline comment
    for each one; for more, apply the directive at the beginning of a block.

.. _main:

3.17 Main 函数
--------------------------------

3.17 Main 

.. tab:: 中文

    在 Python 中，:code:`pydoc` 和单元测试要求模块是可导入的。如果一个文件用于作为可执行文件，它的主要功能应放在 :code:`main()` 函数中，且代码应始终检查 :code:`if __name__ == '__main__'`，以避免在模块导入时执行主程序。

    当使用 `absl <https://github.com/abseil/abseil-py>`_ 时，应使用 :code:`app.run`：

    .. code-block:: python

        from absl import app
        ...

        def main(argv: Sequence[str]):
            # 处理非标志参数
            ...

        if __name__ == '__main__':
            app.run(main)

    否则，使用：

    .. code-block:: python

        def main():
            ...

        if __name__ == '__main__':
            main()

    所有顶层代码在模块被导入时都会执行。小心不要在此时调用函数、创建对象或执行其他操作，特别是在使用 :code:`pydoc` 时。

    倾向于编写小而专注的函数。

    我们承认，有时长函数是合适的，因此并没有对函数的长度设定硬性限制。如果一个函数超过了大约 40 行，考虑是否可以将其拆分，而不影响程序结构。

    即使你的长函数现在能完美工作，几个月后修改它的某人可能会添加新的行为，这可能会导致难以发现的 bug。保持函数简短简单，可以使其他人更容易阅读和修改代码。

    在处理一些代码时，你可能会遇到长而复杂的函数。如果修改这些函数非常困难，或者你发现错误很难调试，或者你希望在不同的上下文中多次使用其中的某部分代码，考虑将函数拆解成更小、更易于管理的块。

.. tab:: 英文

    In Python, :code:`pydoc` as well as unit tests require modules to be importable. If a
    file is meant to be used as an executable, its main functionality should be in a
    :code:`main()` function, and your code should always check :code:`if __name__ == '__main__'`
    before executing your main program, so that it is not executed when the module
    is imported.

    When using  `absl <https://github.com/abseil/abseil-py>`_ , use :code:`app.run`:

    .. code-block:: python

        from absl import app
        ...

        def main(argv: Sequence[str]):
            # process non-flag arguments
            ...

        if __name__ == '__main__':
            app.run(main)

    Otherwise, use:

    .. code-block:: python

        def main():
            ...

        if __name__ == '__main__':
            main()

    All code at the top level will be executed when the module is imported. Be
    careful not to call functions, create objects, or perform other operations that
    should not be executed when the file is being :code:`pydoc` ed.

.. _s3.18-function-length:
.. _318-function-length:

.. _function-length:

3.18 函数长度
--------------------------------

3.18 Function length 

.. tab:: 中文

    倾向于编写小而专注的函数。

    我们承认，有时长函数是合适的，因此并没有对函数的长度设定硬性限制。如果一个函数超过了大约 40 行，考虑是否可以将其拆分，而不影响程序结构。

    即使你的长函数现在能完美工作，几个月后修改它的某人可能会添加新的行为，这可能会导致难以发现的 bug。保持函数简短简单，可以使其他人更容易阅读和修改代码。

    在处理一些代码时，你可能会遇到长而复杂的函数。如果修改这些函数非常困难，或者你发现错误很难调试，或者你希望在不同的上下文中多次使用其中的某部分代码，考虑将函数拆解成更小、更易于管理的块。

.. tab:: 英文

    Prefer small and focused functions.

    We recognize that long functions are sometimes appropriate, so no hard limit is
    placed on function length. If a function exceeds about 40 lines, think about
    whether it can be broken up without harming the structure of the program.

    Even if your long function works perfectly now, someone modifying it in a few
    months may add new behavior. This could result in bugs that are hard to find.
    Keeping your functions short and simple makes it easier for other people to read
    and modify your code.

    You could find long and complicated functions when working with
    some
    code. Do not be intimidated by modifying existing code: if working with such a
    function proves to be difficult, you find that errors are hard to debug, or you
    want to use a piece of it in several different contexts, consider breaking up
    the function into smaller and more manageable pieces.

.. _s3.19-type-annotations:
.. _319-type-annotations:

.. _type-annotations:

3.19 类型注解 
--------------------------------

3.19 Type Annotations 

.. _s3.19.1-general-rules:
.. _s3.19.1-general:
.. _3191-general-rules:

.. _typing-general:

3.19.1 一般规则
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.1 General Rules 

.. tab:: 中文

    * 熟悉 `type hints <https://docs.python.org/3/library/typing.html>`_ 。
    
    * 通常不需要为 :code:`self` 或 :code:`cls` 添加注解。如果为了正确的类型信息需要，可以使用 `Self <https://docs.python.org/3/library/typing.html#typing.Self>`_ ，例如：
    
      .. code-block:: python
      
          from typing import Self
      
          class BaseClass:
              @classmethod
              def create(cls) -> Self:
                  ...
      
              def difference(self, other: Self) -> float:
                  ...
    
    * 同样，不需要为 :code:`__init__` 方法的返回值添加注解（因为 :code:`None` 是唯一有效的返回类型）。
    
    * 如果某个变量或返回类型不应被表达，可以使用 :code:`Any`。
    
    * 并不要求为模块中的所有函数添加注解。
    
      - 至少为公共 API 添加注解。
      - 使用判断力在安全性、清晰度和灵活性之间找到一个良好的平衡。
      - 为易发生类型相关错误的代码（例如历史 bug 或复杂的代码）添加注解。
      - 为难以理解的代码添加注解。
      - 随着代码稳定并且从类型角度变得成熟，可以考虑为所有函数添加注解，而不会失去过多的灵活性。

.. tab:: 英文

    * Familiarize yourself with `type hints <https://docs.python.org/3/library/typing.html>`_ .
    
    * Annotating :code:`self` or :code:`cls` is generally not necessary. `Self <https://docs.python.org/3/library/typing.html#typing.Self>`_  can be used if it is necessary for proper type information, e.g.
    
      .. code-block:: python
      
          from typing import Self
      
          class BaseClass:
          @classmethod
          def create(cls) -> Self:
              ...
      
          def difference(self, other: Self) -> float:
              ...
    
    * Similarly, don't feel compelled to annotate the return value of :code:`__init__`
      (where :code:`None` is the only valid option).
    
    * If any other variable or a returned type should not be expressed, use :code:`Any`.
    
    * You are not required to annotate all the functions in a module.
    
      - At least annotate your public APIs.
      - Use judgment to get to a good balance between safety and clarity on the one hand, and flexibility on the other.
      - Annotate code that is prone to type-related errors (previous bugs or complexity).
      - Annotate code that is hard to understand.
      - Annotate code as it becomes stable from a types perspective. In many cases, you can annotate all the functions in mature code without losing too much flexibility.

.. _s3.19.2-line-breaking:
.. _3192-line-breaking:

.. _typing-line-breaking:

3.19.2 换行
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.2 Line Breaking 

.. tab:: 中文

    尝试遵循现有的 :ref:`缩进 <indentation>` 规则。

    在注解之后，许多函数签名将变成“每行一个参数”。为了确保返回类型也有自己的一行，可以在最后一个参数后添加逗号。

    .. code-block:: python

        def my_method(
            self,
            first_var: int,
            second_var: Foo,
            third_var: Bar | None,
        ) -> int:
        ...

    总是优先在变量之间换行，而不是例如在变量名和类型注解之间换行。但是，如果所有内容都能放在同一行，当然可以这样做。

    .. code-block:: python

        def my_method(self, first_var: int) -> int:
        ...

    如果函数名、最后一个参数和返回类型的组合太长，可以在新的一行进行缩进 4 个空格。当使用换行时，优先将每个参数和返回类型放在单独的行，并使闭括号与 :code:`def` 对齐：

    .. code-block:: python

        Yes:
        def my_method(
            self,
            other_arg: MyLongType | None,
        ) -> tuple[MyLongType1, MyLongType1]:
        ...

    可选地，返回类型也可以放在与最后一个参数相同的行中：

    .. code-block:: python

        Okay:
        def my_method(
            self,
            first_var: int,
            second_var: int) -> dict[OtherLongType, MyLongType]:
        ...

    :code:`pylint` 允许你将闭括号移到新的一行并与开括号对齐，但这样做可读性较差。

    .. code-block:: python

        No:
        def my_method(self,
                    other_arg: MyLongType | None,
                    ) -> dict[OtherLongType, MyLongType]:
        ...

    如上面的示例所示，尽量避免拆分类型。然而，有时类型太长，无法放在一行内（尽量保持子类型不被拆分）。

    .. code-block:: python

        def my_method(
            self,
            first_var: tuple[list[MyLongType1],
                            list[MyLongType2]],
            second_var: list[dict[
                MyLongType3, MyLongType4]],
        ) -> None:
            ...

    如果单一的名称和类型太长，可以考虑为该类型使用 :ref:`别名 <typing-aliases>` 。如果没有其他选择，最后的办法是将其拆分到冒号后并缩进 4 个空格。

    .. code-block:: python

        Yes:
        def my_function(
            long_variable_name:
                long_module_name.LongTypeName,
        ) -> None:
            ...

    .. code-block:: python

        No:
        def my_function(
            long_variable_name: long_module_name.
                LongTypeName,
        ) -> None:
            ...

.. tab:: 英文

    Try to follow the existing `indentation <indentation_>`_ rules.

    After annotating, many function signatures will become "one parameter per line".
    To ensure the return type is also given its own line, a comma can be placed
    after the last parameter.

    .. code-block:: python

        def my_method(
            self,
            first_var: int,
            second_var: Foo,
            third_var: Bar | None,
        ) -> int:
        ...

    Always prefer breaking between variables, and not, for example, between variable
    names and type annotations. However, if everything fits on the same line, go for
    it.

    .. code-block:: python

        def my_method(self, first_var: int) -> int:
        ...

    If the combination of the function name, the last parameter, and the return type
    is too long, indent by 4 in a new line. When using line breaks, prefer putting
    each parameter and the return type on their own lines and aligning the closing
    parenthesis with the :code:`def`:

    .. code-block:: python

        Yes:
        def my_method(
            self,
            other_arg: MyLongType | None,
        ) -> tuple[MyLongType1, MyLongType1]:
        ...

    Optionally, the return type may be put on the same line as the last parameter:

    .. code-block:: python

        Okay:
        def my_method(
            self,
            first_var: int,
            second_var: int) -> dict[OtherLongType, MyLongType]:
        ...

    :code:`pylint` allows you to move the closing parenthesis to a new line and align with the opening one, but this is less readable.

    .. code-block:: python

        No:
        def my_method(self,
                    other_arg: MyLongType | None,
                    ) -> dict[OtherLongType, MyLongType]:
        ...

    As in the examples above, prefer not to break types. However, sometimes they are
    too long to be on a single line (try to keep sub-types unbroken).

    .. code-block:: python

        def my_method(
            self,
            first_var: tuple[list[MyLongType1],
                            list[MyLongType2]],
            second_var: list[dict[
                MyLongType3, MyLongType4]],
        ) -> None:
            ...

    If a single name and type is too long, consider using an
    `alias <typing-aliases_>`_ for the type. The last resort is to break after the
    colon and indent by 4.

    .. code-block:: python

        Yes:
        def my_function(
            long_variable_name:
                long_module_name.LongTypeName,
        ) -> None:
            ...

    .. code-block:: python

        No:
        def my_function(
            long_variable_name: long_module_name.
                LongTypeName,
        ) -> None:
            ...

.. _s3.19.3-forward-declarations:
.. _3193-forward-declarations:

.. _forward-declarations:

3.19.3 前向声明
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.3 Forward Declarations 

.. tab:: 中文

    如果您需要使用尚未定义的类名（来自同一模块） - 例如，如果您需要该类声明中的类名，或者如果您使用稍后在代码中定义的类 - 请使用 :code:`from __future__ import annotations` 或使用字符串作为类名。

.. tab:: 英文

    If you need to use a class name (from the same module) that is not yet defined -- for example, if you need the class name inside the declaration of that class, or if you use a class that is defined later in the code -- either use :code:`from __future__ import annotations` or use a string for the class name.

.. code-block:: python

    Yes:
    from __future__ import annotations

    class MyClass:
        def __init__(self, stack: Sequence[MyClass], item: OtherClass) -> None:

    class OtherClass:
        ...

.. code-block:: python
    Yes:
    class MyClass:
        def __init__(self, stack: Sequence['MyClass'], item: 'OtherClass') -> None:

    class OtherClass:
        ...

.. _s3.19.4-default-values:
.. _3194-default-values:

.. _typing-default-values:

3.19.4 默认值
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.4 Default Values 

.. tab:: 中文

    按照 `PEP-008 <https://peps.python.org/pep-0008/#other-recommendations>`_ ， *仅* 对同时具有类型注释和默认值的参数在 :code:`=` 周围使用空格。

.. tab:: 英文

    As per  `PEP-008 <https://peps.python.org/pep-0008/#other-recommendations>`_ , use spaces around the :code:`=` *only* for arguments that have both a type annotation and a default value.

.. code-block:: python

    Yes:
    def func(a: int = 0) -> int:
        ...

.. code-block:: python

    No:
    def func(a:int=0) -> int:
        ...

.. _s3.19.5-nonetype:
.. _s3.19.5-none-type:
.. _3195-nonetype:

.. _none-type:

3.19.5 NoneType 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.5 NoneType 

.. tab:: 中文

    在 Python 类型系统中，:code:`NoneType` 是“一等”类型，出于类型识别的目的，:code:`None` 是 :code:`NoneType` 的别名。如果参数可以是 :code:`None`，则必须声明！您可以使用 :code:`|` 联合类型表达式（在新的 Python 3.10 及更高版本中推荐使用），或者使用较旧的 :code:`Optional` 和 :code:`Union` 语法。

    使用显式 :code:`X | None` 而不是隐式。早期版本的类型检查器允许将 :code:`a: str = None` 解释为 :code:`a: str | None = None`，但这不再是首选行为。

.. tab:: 英文

    In the Python type system, :code:`NoneType` is a "first class" type, and for typing purposes, :code:`None` is an alias for :code:`NoneType`. If an argument can be :code:`None`, it has to be declared! You can use :code:`|` union type expressions (recommended in new Python 3.10+ code), or the older :code:`Optional` and :code:`Union` syntaxes.

    Use explicit :code:`X | None` instead of implicit. Earlier versions of type checker allowed :code:`a: str = None` to be interpreted as :code:`a: str | None = None`, but that is no longer the preferred behavior.

.. code-block:: python

    Yes:
    def modern_or_union(a: str | int | None, b: str | None = None) -> str:
        ...
    def union_optional(a: Union[str, int, None], b: Optional[str] = None) -> str:
        ...

.. code-block:: python

    No:
    def nullable_union(a: Union[None, str]) -> str:
        ...
    def implicit_optional(a: str = None) -> str:
        ...

.. _s3.19.6-type-aliases:
.. _s3.19.6-aliases:
.. _3196-type-aliases:
.. _typing-aliases:

.. _type-aliases:

3.19.6 类型别名
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.6 Type Aliases 

.. tab:: 中文

    您可以声明复杂类型的别名。别名的名称应首字母大写。如果别名仅在此模块中使用，则应为 _Private。

    请注意，:code:`: TypeAlias` 注释仅在 3.10 及以上版本中受支持。

.. tab:: 英文

    You can declare aliases of complex types. The name of an alias should be CapWorded. If the alias is used only in this module, it should be _Private.

    Note that the :code:`: TypeAlias` annotation is only supported in versions 3.10+.

.. code-block:: python

    from typing import TypeAlias

    _LossAndGradient: TypeAlias = tuple[tf.Tensor, tf.Tensor]
    ComplexTFMap: TypeAlias = Mapping[str, _LossAndGradient]

.. _s3.19.7-ignoring-types:
.. _s3.19.7-ignore:
.. _3197-ignoring-types:

.. _typing-ignore:

3.19.7 忽略类型
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.7 Ignoring Types 

.. tab:: 中文

    您可以使用特殊注释 :code:`# type: ignore` 来禁用某一行的类型检查。

    pytype 有一个针对特定错误的禁用选项（类似于 lint）：

.. tab:: 英文

    You can disable type checking on a line with the special comment :code:`# type: ignore`.

    :code:`pytype` has a disable option for specific errors (similar to lint):

.. code-block:: python

    # pytype: disable=attribute-error


.. _s3.19.8-typing-variables:
.. _s3.19.8-comments:
.. _3198-typing-internal-variables:

.. _typing-variables:

3.19.8 变量类型
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.8 Typing Variables 

.. tab:: 中文

    .. _annotated-assignments:

    :ref:`注解变量 <annotated-assignments>`
        如果一个内部变量的类型难以或不可能推断，请使用带注解的赋值来指定其类型——在变量名和赋值之间使用冒号和类型（与具有默认值的函数参数的做法相同）：
    
        .. code-block:: python
        
            a: Foo = SomeUndecoratedFunction()
    
    .. _type-comments:
    
    `类型注释 <type-comments_>`_
        虽然你可能会在代码库中看到它们（在 Python 3.6 之前是必需的），但不要再在行尾添加 :code:`# type: <类型名>` 注释：

        .. code-block:: python

            a = SomeUndecoratedFunction()  # type: Foo

.. tab:: 英文

    :ref:`Annotated Assignments <annotated-assignments>`
        If an internal variable has a type that is hard or impossible to infer,
        specify its type with an annotated assignment - use a colon and type between
        the variable name and value (the same as is done with function arguments
        that have a default value):

        .. code-block:: python
        
            a: Foo = SomeUndecoratedFunction()
    

    :ref:`type Comments <type-comments>`
        Though you may see them remaining in the codebase (they were necessary
        before Python 3.6), do not add any more uses of a :code:`# type: <type name>`
        comment on the end of the line:

        .. code-block:: python

            a = SomeUndecoratedFunction()  # type: Foo

.. _s3.19.9-tuples-vs-lists:
.. _s3.19.9-tuples:
.. _3199-tuples-vs-lists:

.. _typing-tuples:

3.19.9 元组和列表
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.9 Tuples vs Lists 

.. tab:: 中文

    类型列表只能包含单一类型的对象。类型元组可以包含单一重复类型，也可以包含一定数量的不同类型的元素。后者通常用作函数的返回类型。

.. tab:: 英文

    Typed lists can only contain objects of a single type. Typed tuples can either have a single repeated type or a set number of elements with different types. The latter is commonly used as the return type from a function.

.. code-block:: python

    a: list[int] = [1, 2, 3]
    b: tuple[int, ...] = (1, 2, 3)
    c: tuple[int, str, float] = (1, "2", 3.5)


.. _s3.19.10-typevars:
.. _s3.19.10-type-var:
.. _31910-typevar:
.. _typing-type-var:

.. _typevars:

3.19.10 类型变量
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.10 Type variables 

.. tab:: 中文

    Python 的类型系统支持 `泛型 <https://docs.python.org/3/library/typing.html#generics>`_。使用类型变量（例如 :code:`TypeVar` 和 :code:`ParamSpec`）是泛型的一种常见用法。

    示例：

    .. code-block:: python

        from collections.abc import Callable
        from typing import ParamSpec, TypeVar
        _P = ParamSpec("_P")
        _T = TypeVar("_T")
        ...

        def next(l: list[_T]) -> _T:
            return l.pop()

        def print_when_called(f: Callable[_P, _T]) -> Callable[_P, _T]:
            def inner(*args: _P.args, **kwargs: _P.kwargs) -> _T:
                print("Function was called")
                return f(*args, **kwargs)
            return inner

    类型变量（:code:`TypeVar`）可以被限制为特定类型：

    .. code-block:: python

        AddableType = TypeVar("AddableType", int, float, str)
        def add(a: AddableType, b: AddableType) -> AddableType:
            return a + b

    在 :code:`typing` 模块中，一个常见的预定义类型变量是 :code:`AnyStr`。当多个注解可能是 :code:`bytes` 或 :code:`str` 并且它们必须是相同类型时，可以使用它。

    .. code-block:: python
        
        from typing import AnyStr

        def check_length(x: AnyStr) -> AnyStr:
            if len(x) <= 42:
                return x
            raise ValueError()

    类型变量的命名必须具有描述性，除非满足以下所有条件：

    *   不对外可见；
    *   没有类型限制；

    .. code-block:: python

        Yes:
            _T = TypeVar("_T")
            _P = ParamSpec("_P")
            AddableType = TypeVar("AddableType", int, float, str)
            AnyFunction = TypeVar("AnyFunction", bound=Callable)

    .. code-block:: python

        No:
            T = TypeVar("T")
            P = ParamSpec("P")
            _T = TypeVar("_T", int, float, str)
            _F = TypeVar("_F", bound=Callable)

.. tab:: 英文

    The Python type system has `generics <https://docs.python.org/3/library/typing.html#generics>`_. A type variable, such as :code:`TypeVar` and :code:`ParamSpec`, is a common way to use them.

    Example:

    .. code-block:: python

        from collections.abc import Callable
        from typing import ParamSpec, TypeVar
        _P = ParamSpec("_P")
        _T = TypeVar("_T")
        ...

        def next(l: list[_T]) -> _T:
            return l.pop()

        def print_when_called(f: Callable[_P, _T]) -> Callable[_P, _T]:
            def inner(*args: _P.args, **kwargs: _P.kwargs) -> _T:
                print("Function was called")
                return f(*args, **kwargs)
            return inner


    A :code:`TypeVar` can be constrained:

    .. code-block:: python

        AddableType = TypeVar("AddableType", int, float, str)
        def add(a: AddableType, b: AddableType) -> AddableType:
            return a + b

    A common predefined type variable in the :code:`typing` module is :code:`AnyStr`. Use it for
    multiple annotations that can be :code:`bytes` or :code:`str` and must all be the same type.

    .. code-block:: python
        
        from typing import AnyStr

        def check_length(x: AnyStr) -> AnyStr:
            if len(x) <= 42:
                return x
            raise ValueError()

    A type variable must have a descriptive name, unless it meets all of the
    following criteria:

    *   not externally visible
    *   not constrained

    .. code-block:: python

        Yes:
            _T = TypeVar("_T")
            _P = ParamSpec("_P")
            AddableType = TypeVar("AddableType", int, float, str)
            AnyFunction = TypeVar("AnyFunction", bound=Callable)

    .. code-block:: python

        No:
            T = TypeVar("T")
            P = ParamSpec("P")
            _T = TypeVar("_T", int, float, str)
            _F = TypeVar("_F", bound=Callable)

.. _s3.19.11-string-types:
.. _s3.19.11-strings:
.. _31911-string-types:

.. _typing-strings:

3.19.11 字符类型
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.11 String types 

.. tab:: 中文

    .. warning::

        不要在新代码中使用 :code:`typing.Text`。它仅用于兼容 Python 2/3。

    处理字符串/文本数据时使用 :code:`str`，处理二进制数据时使用 :code:`bytes`。

    .. code-block:: python

        def deals_with_text_data(x: str) -> str:
            ...
        def deals_with_binary_data(x: bytes) -> bytes:
            ...

    如果一个函数中的所有字符串类型总是相同，例如返回类型与参数类型一致（如上例所示），请使用 :ref:`AnyStr <typing-type-var>`。

.. tab:: 英文

    .. warning::
        
        Do not use :code:`typing.Text` in new code. It's only for Python 2/3 compatibility.

    Use :code:`str` for string/text data. For code that deals with binary data, use :code:`bytes`.

    .. code-block:: python

        def deals_with_text_data(x: str) -> str:
            ...
        def deals_with_binary_data(x: bytes) -> bytes:
            ...


    If all the string types of a function are always the same, for example if the
    return type is the same as the argument type in the code above, use
    `AnyStr <typing-type-var_>`_.

.. _s3.19.12-imports-for-typing:
.. _s3.19.12-imports:
.. _31912-imports-for-typing:

.. _typing-imports:

3.19.12 类型的导入 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.12 Imports For Typing 

.. tab:: 中文

    对于来自 :code:`typing` 或 :code:`collections.abc` 模块、用于静态分析和类型检查的符号（包括类型、函数和常量）：

    始终显式导入这些符号本身。这种方式可以让常见注解更简洁，并与全球范围内的类型注解实践保持一致。你可以在一行中从 :code:`typing` 和 :code:`collections.abc` 中导入多个具体符号，例如：

    .. code-block:: python

        from collections.abc import Mapping, Sequence
        from typing import Any, Generic, cast, TYPE_CHECKING

    由于这种导入方式会将名称添加到本地命名空间中，因此应将 :code:`typing` 和 :code:`collections.abc` 中的名称视为关键字，不应在你的 Python 代码中再次定义（无论是否使用类型注解）。如果类型名与模块中已有名称冲突，应使用 :code:`import x as y` 的方式导入：

    .. code-block:: python

        from typing import Any as AnyType

    在注解函数签名时，优先使用抽象容器类型（如 :code:`collections.abc.Sequence`），而不是具体类型（如 :code:`list`）。如果必须使用具体类型（例如一个带类型元素的元组），请优先使用内建类型（如 :code:`tuple`），而不是 :code:`typing` 模块中的参数化类型别名（如 :code:`typing.Tuple`）。

.. tab:: 英文

    For symbols (including types, functions, and constants) from the :code:`typing` or
    :code:`collections.abc` modules used to support static analysis and type checking,
    always import the symbol itself. This keeps common annotations more concise and
    matches typing practices used around the world. You are explicitly allowed to
    import multiple specific symbols on one line from the :code:`typing` and
    :code:`collections.abc` modules. For example:

    .. code-block:: python

        from collections.abc import Mapping, Sequence
        from typing import Any, Generic, cast, TYPE_CHECKING


    Given that this way of importing adds items to the local namespace, names in
    :code:`typing` or :code:`collections.abc` should be treated similarly to keywords, and not
    be defined in your Python code, typed or not. If there is a collision between a
    type and an existing name in a module, import it using :code:`import x as y`.

    .. code-block:: python

        from typing import Any as AnyType

    When annotating function signatures, prefer abstract container types like
    :code:`collections.abc.Sequence` over concrete types like :code:`list`. If you need to use a
    concrete type (for example, a :code:`tuple` of typed elements), prefer built-in types
    like :code:`tuple` over the parametric type aliases from the :code:`typing` module (e.g.,
    :code:`typing.Tuple`).

.. code-block:: python

    from typing import List, Tuple

    def transform_coordinates(original: List[Tuple[float, float]]) -> List[Tuple[float, float]]:
        ...

.. code-block:: python

    from collections.abc import Sequence

    def transform_coordinates(original: Sequence[tuple[float, float]]) -> Sequence[tuple[float, float]]:
        ...


.. _s3.19.13-conditional-imports:
.. _31913-conditional-imports:

.. _typing-conditional-imports:

3.19.13 条件导入 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.13 Conditional Imports 

.. tab:: 中文

    仅在特殊情况下才使用条件导入（conditional imports），即在运行时必须避免引入额外的类型检查所需导入时。此模式并不推荐，更推荐通过重构使导入可以放在顶层。

    仅用于类型注解的导入可以放入 :code:`if TYPE_CHECKING:` 块中：

    - 条件导入的类型必须使用字符串形式引用，以兼容 Python 3.6（在该版本中注解表达式会被实际求值）；
    - 仅将用于类型注解的实体定义在此块中（包括别名），否则在运行时会出现模块未导入的错误；
    - 此块应紧随所有常规导入之后；
    - 类型导入列表中不应有空行；
    - 按照常规导入的排序方式对其排序。

.. tab:: 英文

    Use conditional imports only in exceptional cases where the additional imports
    needed for type checking must be avoided at runtime. This pattern is
    discouraged; alternatives such as refactoring the code to allow top-level
    imports should be preferred.

    Imports that are needed only for type annotations can be placed within an :code:`if TYPE_CHECKING:` block.

    - Conditionally imported types need to be referenced as strings, to be forward compatible with Python 3.6 where the annotation expressions are actually evaluated.
    - Only entities that are used solely for typing should be defined here; this includes aliases. Otherwise it will be a runtime error, as the module will not be imported at runtime.
    - The block should be right after all the normal imports.
    - There should be no empty lines in the typing imports list.
    - Sort this list as if it were a regular imports list.

.. code-block:: python

    import typing
    if typing.TYPE_CHECKING:
        import sketch
    def f(x: "sketch.Sketch"): ...


.. _s3.19.14-circular-dependencies:
.. _s3.19.14-circular-deps:
.. _31914-circular-dependencies:

.. _typing-circular-deps:

3.19.14 循环依赖
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.14 Circular Dependencies 

.. tab:: 中文

    由类型注解引起的循环依赖（circular dependencies）是一种代码异味（code smell）。这类代码通常是重构的良好候选。尽管从技术上讲可以保留循环依赖，但许多构建系统并不允许这样做，因为每个模块都必须相互依赖。

    应将导致循环依赖导入的模块替换为 :code:`Any`。使用一个具有语义意义的 :ref:`别名 <typing-aliases>` ，并在当前模块中使用真实类型名（由于 :code:`Any` 的任何属性都是 :code:`Any`）。别名定义应与最后一个 import 之间用一个空行分隔。

    .. code-block:: python

        from typing import Any

        some_mod = Any  # some_mod.py 导入了此模块
        ...

        def my_method(self, var: "some_mod.SomeType") -> None:
            ...

.. tab:: 英文

    Circular dependencies that are caused by typing are code smells. Such code is a
    good candidate for refactoring. Although technically it is possible to keep
    circular dependencies, various build systems will not let you do so
    because each module has to depend on the other.

    Replace modules that create circular dependency imports with :code:`Any`. Set an
    `alias <typing-aliases_>`_ with a meaningful name, and use the real type name from
    this module (any attribute of :code:`Any` is :code:`Any`). Alias definitions should be
    separated from the last import by one line.

    .. code-block:: python

        from typing import Any

        some_mod = Any  # some_mod.py imports this module.
        ...

        def my_method(self, var: "some_mod.SomeType") -> None:
            ...

.. _typing-generics:
.. _s3.19.15-generics:
.. _31915-generics:

.. _generics:

3.19.15 范型 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

3.19.15 Generics 

.. tab:: 中文

    在使用泛型类型进行注解时，应优先在参数列表中显式指定类型参数；否则，这些泛型的参数将被视为 `Any <https://docs.python.org/3/library/typing.html#the-any-type>`_ 。

    .. code-block:: python

        # 推荐：
        def get_names(employee_ids: Sequence[int]) -> Mapping[int, str]:
            ...

    .. code-block:: python
        
        # 不推荐：
        # 这会被解释为：get_names(employee_ids: Sequence[Any]) -> Mapping[Any, Any]
        def get_names(employee_ids: Sequence) -> Mapping:
            ...

    如果泛型的最佳类型参数确实是 :code:`Any`，请显式声明；但在许多情况下，使用 :ref:`TypeVar <typing-type-var>` 会更合适：

    .. code-block:: python

        # 不推荐：
        def get_names(employee_ids: Sequence[Any]) -> Mapping[Any, str]:
            """根据给定 ID 返回 employee ID 到姓名的映射。"""

    .. code-block:: python

        # 推荐：
        _T = TypeVar('_T')
        def get_names(employee_ids: Sequence[_T]) -> Mapping[_T, str]:
            """根据给定 ID 返回 employee ID 到姓名的映射。"""

.. tab:: 英文

    When annotating, prefer to specify type parameters for
    `generic <https://docs.python.org/3/library/typing.html#generics>`_ types in a
    parameter list; otherwise, the generics' parameters will be assumed to be
    `Any <https://docs.python.org/3/library/typing.html#the-any-type>`_ .

    .. code-block:: python

        # Yes:
        def get_names(employee_ids: Sequence[int]) -> Mapping[int, str]:
            ...

    .. code-block:: python
        
        # No:
        # This is interpreted as get_names(employee_ids: Sequence[Any]) -> Mapping[Any, Any]
        def get_names(employee_ids: Sequence) -> Mapping:
            ...

    If the best type parameter for a generic is :code:`Any`, make it explicit, but
    remember that in many cases `TypeVar <typing-type-var_>`_ might be more
    appropriate:

    .. code-block:: python

        # No:
        def get_names(employee_ids: Sequence[Any]) -> Mapping[Any, str]:
            """Returns a mapping from employee ID to employee name for given IDs."""

    .. code-block:: python

        # Yes:
        _T = TypeVar('_T')
        def get_names(employee_ids: Sequence[_T]) -> Mapping[_T, str]:
            """Returns a mapping from employee ID to employee name for given IDs."""


.. _4-parting-words:

.. _consistency:

4 告别辞
=======================

4 Parting Words 

.. tab:: 中文

    *保持一致*.

    如果您正在编辑代码，请花几分钟时间查看周围的代码并确定其样式。如果他们在索引变量名中使用 :code:`_idx` 后缀，您也应该这样做。如果他们的注释周围有小方框，请也让您的注释周围也使用小方框。

    制定样式指南的目的是为了形成一套通用的代码词汇表，这样人们就能专注于你所说的内容，而不是你如何表达。我们在这里提供全局样式规则，以便人们了解这些词汇表，但局部样式也同样重要。如果你添加到文件中的代码看起来与周围现有的代码截然不同，那么读者在阅读时就会感到不知所措。

    然而，一致性是有局限性的。它更多地适用于局部情况以及全局样式未指定的选择。一致性通常不应被用作沿用旧样式的理由，而不考虑新样式的优势，也不应考虑代码库随着时间的推移趋向于新样式的趋势。

.. tab:: 英文

    *BE CONSISTENT*.

    If you're editing code, take a few minutes to look at the code around you and
    determine its style. If they use :code:`_idx` suffixes in index variable names, you
    should too. If their comments have little boxes of hash marks around them, make
    your comments have little boxes of hash marks around them too.

    The point of having style guidelines is to have a common vocabulary of coding so
    people can concentrate on what you're saying rather than on how you're saying
    it. We present global style rules here so people know the vocabulary, but local
    style is also important. If code you add to a file looks drastically different
    from the existing code around it, it throws readers out of their rhythm when
    they go to read it.

    However, there are limits to consistency. It applies more heavily locally and on
    choices unspecified by the global style. Consistency should not generally be
    used as a justification to do things in an old style without considering the
    benefits of the new style, or the tendency of the codebase to converge on newer
    styles over time.

