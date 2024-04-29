# Java Email Service (Version 2.0)

This Java project provides email sending functionality using different email service configurations, including Mailtrap and Gmail. It consists of several classes designed to handle email composition, attachment embedding, and session management.

## What's New in Version 2.0

### `MessageHandler` (Builder Pattern)

Version 2.0 introduces the `MessageHandler` class, which provides a flexible and fluent interface for creating email messages. This class implements the Builder Pattern, allowing users to construct emails by specifying different components (sender, recipient, subject, body, attachments, etc.) in a clear and concise manner.

## Project Structure

The project includes the following main classes:

1. **MailtrapServiceHandler**: Implements the `MailtrapService` interface to send emails using Mailtrap's SMTP server configuration.

2. **EmailServiceHandler**: Implements the `EmailService` interface to send emails using Gmail's SMTP server configuration.

3. **MessageHandler**: Handles the creation and management of email messages using JavaMail API, implementing the Builder Pattern.

4. **EmailValidator**: Provides utility methods for email validation using regular expressions.

## Design Patterns

- **Singleton Pattern**: Both `MailtrapServiceHandler` and `EmailServiceHandler` classes use the singleton pattern to ensure that only one instance of the service handler is created throughout the application.

- **Builder Pattern**: The `MessageHandler` class utilizes the builder pattern to construct complex email messages step by step.

## Classes Overview

### `MailtrapServiceHandler`

- **Purpose**: Provides email sending functionality using Mailtrap's SMTP server.

- **Methods**:
    - `getInstance()`: Returns the singleton instance of `MailtrapServiceHandler`.
    - `sendEmail()`: Sends an email with text content using Mailtrap configuration.
    - `sendImage()`: Sends an email with an embedded image using Mailtrap configuration.
    - `sendFile()`: Sends an email with a file attachment using Mailtrap configuration.

### `EmailServiceHandler`

- **Purpose**: Provides email sending functionality using Gmail's SMTP server.

- **Methods**:
    - `getInstance()`: Returns the singleton instance of `EmailServiceHandler`.
    - `sendEmail()`: Sends an email with text content using Gmail configuration.
    - `sendImage()`: Sends an email with an embedded image using Gmail configuration.
    - `sendFile()`: Sends an email with a file attachment using Gmail configuration.

### `MessageHandler`

- **Purpose**: Handles the creation and management of email messages using JavaMail API, implementing the Builder Pattern.

- **Design Pattern**:
    - **Builder Pattern**: Provides a fluent interface to construct email messages with optional parts.

- **Methods**:
    - `from()`: Specifies the sender's email address.
    - `to()`: Specifies the recipient's email address.
    - `subject()`: Specifies the email subject.
    - `text()`: Specifies the plain text body content.
    - `image()`: Embeds an image in the email message.
    - `images()`: Embeds an images in the email message.
    - `file()`: Embeds an file in the email message.
    - `files()`: Embeds an files in the email message.

### `EmailValidator`

- **Purpose**: Utility class for email validation using regular expressions.

- **Methods**:
    - `isValid(ValidConfiguration validConfiguration, String email)`: Validates an email address against a specified `ValidConfiguration` pattern.
    - `isValid(String pattern, String email)`: Validates an email address against a custom regular expression pattern.

## ValidConfiguration Interface

The `ValidConfiguration` interface defines valid configuration constants for email validation. It provides a set of regular expressions (regex) to validate email addresses.

### `ValidConfiguration` Constants

1. **REGEX_1**: Regular expression based on the official email address format.
2. **REGEX_2**: Simple format regex checking for basic structure.
3. **REGEX_3**: More restrictive format regex for email validation.
4. **REGEX_4**: Covers a broad range of valid email formats.

## How to Use

1. **Import the JAR File**: Include the JAR file containing these classes in your Java project.

2. **Initialize Service Handlers**:
   ```java
   // Using Mailtrap
   MailtrapServiceHandler mailtrapService = MailtrapServiceHandler.getInstance();
   
   // Using Gmail
   EmailServiceHandler gmailService = EmailServiceHandler.getInstance();
   
   mailtrapService.send...(...)
   gmailService.send...(...)
   
   // Using MessageHandler with Builder Pattern
   MessageHandler message = new MessageHandler.Builder()
   .from(senderEmail) // important
   .to(recipientEmail) // important
   .subject(emailSubject) // important
   .text(plainTextContent) // important
   .image(imagePath, imageWidth) // not important
   .images(List<Path>) // not important
   .file(path) // not important
   .files(List<Path>)  // not important
   .build();
   
   message.send()
   
