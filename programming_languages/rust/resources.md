## Resources

<br>

| Name                                                                   | Release date       | Format             | Link                                                                |
| ---                                                                    | ---                | ---                | ---                                                                 |
| [The Rust Programming Language](#the-rust-programming-language)        |  Dec. 22           | Book               | [🔗](https://nostarch.com/rust-programming-language-2nd-edition)    |

<br>

---

<br>

## The Rust Programming Language

<br>

- **Getting started**
  - Installation
    - [Installing rustup on macOs](./files/getting_started/installation/install_on_macOs.md)
    - [Troubleshooting](./files/getting_started/installation/troubleshooting.md)
    - [Updating and uninstalling](./files/getting_started/installation/update_uninstall.md)
    - [Local documentation](./files/getting_started/installation/local_documentation.md)
  - Hello, Wolrd!
    - [Creating a project directory](./files/getting_started/hello_world/creating_project_directory.md)
    - [Writing a running a Rust program](./files/getting_started/hello_world/write_and_run.md)
    - [Anatomy of a Rust program](./files/getting_started/hello_world/program_anatomy.md)
    - [Compiling and running are separate steps](./files/getting_started/hello_world/compile_run.md)
  - Hello, Cargo!
    - [Creating a project with Cargo](./files/getting_started/hello_cargo/create_cargo_project.md)
    - [Building and running a Cargo project](./files/getting_started/hello_cargo/build_and_run.md)
    - [Building for release](./files/getting_started/hello_cargo/build_for_release.md)

- **Common programming concepts**
  - Variable and mutability
    - [Constants](./files/common_programming_concepts/variable_mutability/constants.md)
    - [Shadowing](./files/common_programming_concepts/variable_mutability/shadowing.md)
  - Data types
    - [Scalar types](./files/common_programming_concepts/data_types/scalar_type.md)
    - [Compound types](./files/common_programming_concepts/data_types/compound_type.md)
  - Functions
    - [Parameters](./files/common_programming_concepts/functions/parameters.md)
    - [Statements and expressions](./files/common_programming_concepts/functions/statements_expressions.md)
    - [Function with return values](./files/common_programming_concepts/functions/return_value.md)
  - [Comment](./files/common_programming_concepts/comments.md)
  - Control flow
    - [If expressions](./files/common_programming_concepts/control_flow/if_expression.md)
    - [Repetition with loops](./files/common_programming_concepts/control_flow/repetition_loops.md)

- **Understanding ownership**
  - What is ownership
    - [Ownership rules](./files/understanding_ownership/what_is_ownership/ownership_rules.md)
    - [Variable scope](./files/understanding_ownership/what_is_ownership/variable_scope.md)
    - [The string type](./files/understanding_ownership/what_is_ownership/string_type.md)
    - [Memory and allocation](./files/understanding_ownership/what_is_ownership/memory_allocation.md)
    - [Ownership and functions](./files/understanding_ownership/what_is_ownership/ownership_functions.md)
    - [Return value and scope](./files/understanding_ownership/what_is_ownership/return_value_scope.md)
  - References and borrowing
    - [Mutable references](./files/understanding_ownership/references_borrowing/mutable_references.md)
    - [Dangling references](./files/understanding_ownership/references_borrowing/dangling_references.md)
    - [The rule of references](./files/understanding_ownership/references_borrowing/rule_of_references.md)
  - The slice type
    - [String slice](./files/understanding_ownership/slice_type/string_slice.md)
    - [Other slices](./files/understanding_ownership/slice_type/other_slice.md)

- **Using structs to structure related data**
  - Defining and intantiating structs
    - [Using the field init shortand](./files/structs_for_related_data/defining_instantiating/field_init_shorthand.md)
    - [Creating instances from other instances with struct update syntax](./files/structs_for_related_data/defining_instantiating/instances_from_others.md)
    - [Using tuple structs without named fields to create different types](./files/structs_for_related_data/defining_instantiating/tuple_struct_for_types.md)
    - [Unit like struct without any field](./files/structs_for_related_data/defining_instantiating/unit_like_struct_without_field.md)
  - An example of program using structs
    - [Refactoring with tuples](./files/structs_for_related_data/struct_example/refactoring_with_tuples.md)
    - [Refactoring with structs : adding more meaning](./files/structs_for_related_data/struct_example/refactoring_with_structs.md)
    - [Adding useful functionality with derived traits](./files/structs_for_related_data/struct_example/funcs_with_derived_traits.md)
  - Method syntax
    - [Defining methods](./files/structs_for_related_data/method_syntax/defining_methods.md)
    - [Methods with more parameters](./files/structs_for_related_data/method_syntax/method_paramaters.md)
    - [Associated functions](./files/structs_for_related_data/method_syntax/associated_functions.md)
    - [Multiple impl blocks](./files/structs_for_related_data/method_syntax/multiple_impl_blocks.md)

- **Enums and pattern matching**
  - Defining an Enum
    - [Enum values](./files/enums_pattern_matching/defining_enum/enum_values.md)
    - [The option enum and its advantages over null values](./files/enums_pattern_matching/defining_enum/option_enum.md)
  - The match control-flow construct
    - [Patterns that bind to values](./files/enums_pattern_matching/match_control_flow/bind_to_value_pattern.md)
    - [Matching with `Option<T>`](./files/enums_pattern_matching/match_control_flow/Option<T>_matching.md)
    - [Matches are exhaustive](./files/enums_pattern_matching/match_control_flow/exhaustive_matches.md)
    - [Catch-all pattern and the `_` placeholder](./files/enums_pattern_matching/match_control_flow/Catch-All_pattern.md)
  - [Concise control-flow with if let](./files/enums_pattern_matching/concise_if_let.md)

- **Managing growing projects with packages, crates and modules**
  - [Packages and crates](./files/packages_crates_modules/packages_crates.md)
  - [Defining modules to control scope and privacy](./files/packages_crates_modules/module_scope_privacy.md)
  - Paths for reffering to an item in the module tree
    - [Exposing paths with the pub keyword](./files/packages_crates_modules/path_module_tree/exposing_with_pub.md)
    - [Starting relative paths with super](./files/packages_crates_modules/path_module_tree/relative_path_with_super.md)
    - [Making structs and enums public](./files/packages_crates_modules/path_module_tree/structs_enums_public.md)
  - Bringing paths into scope with the use keyword
    - [Creating idiomatic use paths](./files/packages_crates_modules/path_with_use/idiomatic_use_paths.md)
    - [Providing new names with the as keyword](./files/packages_crates_modules/path_with_use/naming_with_as.md)
    - [Re-exporting names with the pub use](./files/packages_crates_modules/path_with_use/re-exporting_pub_use.md)
    - [Using extrnal packages](./files/packages_crates_modules/path_with_use/external_packages.md)
    - [Using nested paths to clean up large use lists](./files/packages_crates_modules/path_with_use/nested_paths.md)
    - [The glob operator](./files/packages_crates_modules/path_with_use/glob_operator.md)
  - [Separating modules into different files](./files/packages_crates_modules/module_separation.md)

- **Common collections**
  - Storing list of values with Vectors
    - [Creating a new vector](./files/common_collections/vectors/creating_vector.md)
    - [Updating a vector](./files/common_collections/vectors/updating_vector.md)
    - [Reading elements of vectors](./files/common_collections/vectors/reading_vector.md)
    - [Iterating over the values in a vector](./files/common_collections/vectors/vector_iteration.md)
    - [Using an Enum to store values in a vector](./files/common_collections/vectors/enums_for_types.md)
    - [Dropping a vector drops its elements](./files/common_collections/vectors/dropping_vector.md)
  - Storing UTF-8 encoded text using strings
    - [What is a string](./files/common_collections/strings/string_definition.md)
    - [Creating a new string](./files/common_collections/strings/string_creation.md)
    - [Updating a string](./files/common_collections/strings/string_updating.md)
    - [Indexing into strings](./files/common_collections/strings/string_indexing.md)
    - [Slicing strings](./files/common_collections/strings/string_slicing.md)
    - [Methods for iterating over strings](./files/common_collections/strings/string_iteration.md)
    - [String are not so simple](./files/common_collections/strings/string_complexity.md)
  - Storing keys with associated values in HashMap
    - [Creating a new HashMap](./files/common_collections/hashmaps/hashmap_creation.md)
    - [Accessing values in a HashMap](./files/common_collections/hashmaps/hashmap_value_access.md)
    - [HashMap and ownership](./files/common_collections/hashmaps/hashmap_ownership.md)
    - [Updating a HashMap](./files/common_collections/hashmaps/hashmap_updating.md)
    - [Hashing functions](./files/common_collections/hashmaps/hashing_functions.md)

- **Error handling**
  - [Unrecoverable errors with panic!](./files/error_handling/unrecoverable_panic!.md)
  - Recoverable errors with Result
    - [Matching on different errors](./files/error_handling/recoverable_result/error_matching.md)
    - [Propagating errors](./files/error_handling/recoverable_result/propagating_errors.md)
  - To panic! or not to panic!
    - [Examples, prototype code, and tests](./files/error_handling/panic!_or_not/ex_proto_code_test.md)
    - [Cases in which you have more information that the compiler](./files/error_handling/panic!_or_not/off_compiler_cases.md)
    - [Guidelines for error handling](./files/error_handling/panic!_or_not/error_handling_guidelines.md)
    - [Creating custom types for validation](./files/error_handling/panic!_or_not/custom_type_for_validation.md)
