# 04. Functional vs Non-Functional Requirements

## Overview

In system design, understanding the difference between functional and non-functional requirements is crucial for building effective systems that meet user needs and business goals. This lesson will define both types of requirements, explain their significance, and provide examples to illustrate how they apply in the context of system design.

## What are Functional Requirements?

**Definition**: Functional requirements specify what a system should do. They describe the functionalities and features that the system must provide to fulfill user needs. These requirements outline the expected behavior of the system in various scenarios.

### Characteristics of Functional Requirements

1. **Specificity**: Functional requirements should be clear and unambiguous, detailing exactly what the system must accomplish.
2. **Measurable**: They should be quantifiable, allowing for testing and validation to ensure that the system meets the specified requirements.
3. **User-Centric**: Functional requirements are often derived from user stories or use cases, focusing on the needs and expectations of end-users.

### Examples of Functional Requirements

- **User Authentication**: The system must allow users to register, log in, and log out securely.
- **Data Entry**: The system must enable users to input and save data in a structured format.
- **Search Functionality**: The system must provide users with the ability to search for specific records or information based on various criteria.
- **Reporting**: The system must generate reports based on user-defined parameters and display them in a user-friendly format.

## What are Non-Functional Requirements?

**Definition**: Non-functional requirements specify how a system should behave and outline the quality attributes that the system must possess. They define the criteria that judge the operation of a system, rather than the specific behaviors.

### Characteristics of Non-Functional Requirements

1. **Quality Attributes**: Non-functional requirements focus on the quality and performance of the system, such as usability, reliability, and security.
2. **Broad Scope**: They often encompass various aspects of the system, including performance, scalability, security, and maintainability.
3. **Impact on User Experience**: Non-functional requirements significantly affect the overall user experience and satisfaction with the system.

### Examples of Non-Functional Requirements

- **Performance**: The system must respond to user requests within 2 seconds under normal load conditions.
- **Scalability**: The system must be able to handle up to 10,000 concurrent users without degradation in performance.
- **Security**: The system must implement encryption for sensitive data and comply with industry security standards.
- **Usability**: The system must be intuitive and easy to navigate, allowing users to complete tasks with minimal training.

## Importance of Distinguishing Between Functional and Non-Functional Requirements

Understanding the distinction between functional and non-functional requirements is critical for several reasons:

1. **Comprehensive Design**: Both types of requirements must be considered during the design phase to ensure that the system meets both user needs and quality standards.
2. **Balanced Prioritization**: Focusing solely on functional requirements may lead to a system that works well but is slow, insecure, or difficult to use. Non-functional requirements help balance the system's functionality with performance and user experience.
3. **Testing and Validation**: Clearly defined requirements enable effective testing strategies. Functional requirements guide the development of test cases that verify system behavior, while non-functional requirements help assess system performance and quality.

## Conclusion

In this lesson, we have explored the concepts of functional and non-functional requirements, highlighting their definitions, characteristics, and importance in system design. Understanding these requirements is essential for creating systems that not only meet user expectations but also deliver quality and performance.

Next: [02. Scalability](./02-scalability.md)
