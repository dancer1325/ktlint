* Ktlint
  * 's properties 
    * are defined |
      * [.editorconfig](https://editorconfig.org/)
        * 👀limited set of `.editorconfig`'s properties define ADDITIONAL configuration 👀
        * ⚠️[AFTER encountering a space | list, ignores sections](https://github.com/editorconfig/editorconfig/issues/148) -> [ktlint issue](https://github.com/pinterest/ktlint/issues/762)⚠️
          * Reason: 🧠`.editorconfig` library used -- by -- `ktlint`🧠
      * IntelliJ IDEA
        * ⚠️ADDITIONAL space BETWEEN glob statements⚠️
          * _Example:_ `[*{kt, kts}]` -- instead of -- `[*{kt,kts}]`
          * Reason: 🧠[IntelliJ IDEA autoformat issue regarding `.editorconfig`](https://youtrack.jetbrains.com/issue/IDEA-242506)🧠
      * custom properties
    * can be overridden
    * if value NOT EXPLICITLY defined -> default value

## Disable rule(s)

* rule sets
  * 👀enable / disable ALL rule set's rules👀
  * 💡`ktlint_ruleSetId`💡
    * rule set property's name
    * _Example:_
    ```.editorconfig
    ktlint_standard = disabled         # disable ALL standard` rule set's ( / provided by KtLint) rules
    ktlint_experimental = enabled      # enable ALL rule sets' ( / provided by KtLint OR OTHER rule providers) ALL `experimental` rules
    ktlint_custom-rule-set = enabled   # enable ALL custom-rule-set` rule set's rules
    ```

* rule property
  * enable / disable an individual rule
    * ⚠️'s precedence > rule sets' precedence⚠️
      * == applied AFTER applying the *rule set* properties
  * 💡`ktlint_ruleSetId_ruleId`💡
    * rule property's name
    * _Example:_
    ```.editorconfig
    ktlint_standard_final-newline = disabled             # disables the `final-newline` rule -- provided by -- KtLint
    ktlint_standard_some-experimental-rule = enabled     # enables the `standard` rule set's ( / provided by KtLint) `some-experimental-rule` rule 
    ktlint_custom-rule-set_custom-rule = disabled        # disables the `custom-rule-set` rule set's ( / NOT provided by KtLint) `custom-rule` rule 
    ```

## Rule's specific configuration settings

* uses
  * configure specific rule's behavior 

* requirements
  * corresponding rule is enabled

| Configuration setting                                                                     | Rule                                                                                  |
|:------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------|
| ij_kotlin_allow_trailing_comma                                                            | [trailing-comma-on-declaration-site](standard.md#trailing-comma-on-declaration-site) |
| ij_kotlin_allow_trailing_comma_on_call_site                                               | [trailing-comma-on-call-site](standard.md#trailing-comma-on-call-site)               |
| ij_kotlin_imports_layout                                                                  | [import-ordering](standard.md#import-ordering)                                       |
| ij_kotlin_packages_to_use_import_on_demand                                                | [no-wildcard-imports](standard.md#no-wildcard-imports)                               |
| indent_size                                                                               | [indent](standard.md#indentation)                                                    |                                                                                       |
| indent_style                                                                              | [indent](standard.md#indentation)                                                    |                                                                                       |
|
| insert_final_newline                                                                      | [final-newline](standard.md#final-newline)                                           |                                                                                       |
| ktlint_chain_method_rule_force_multiline_when_chain_operator_count_greater_or_equal_than  | [chain-method-continuation](../experimental/#chain-method-continuation)               |
| ktlint_class_signature_rule_force_multiline_when_parameter_count_greater_or_equal_than    | [class-signature](../experimental/#class-signature)                                   |
| ktlint_ignore_back_ticked_identifier                                                      | [max-line-length](standard.md#max-line-length)                                       |
| ktlint_function_naming_ignore_when_annotated_with                                         | [function-naming](standard.md#function-naming)                                       |
| ktlint_function_signature_body_expression_wrapping                                        | [function-signature](standard.md#function-signature)                                 |
| ktlint_function_signature_rule_force_multiline_when_parameter_count_greater_or_equal_than | [function-signature](standard.md#function-signature)                                 |
| max_line_length                                                                           | [max-line-length](standard.md#max-line-length) and several other rules               |

## Override Editorconfig properties | specific directories

* [editorconfig's documentation](https://editorconfig.org/#file-format-details)
* _Example:_

    ```.editorconfig
    [*.{kt,kts}]
    ktlint_standard_import-ordering = disabled
    
    [api/*.{kt,kts}]                   # specific directories 
    ktlint_standard_indent = disabled
    ```
