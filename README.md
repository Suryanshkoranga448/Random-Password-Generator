# 🔐 Random Password Generator

A simple and beginner-friendly **Random Password Generator** built using Python.

This project generates random passwords using a combination of letters, numbers, and special characters. The user can enter the required password length, and the program generates a password accordingly.

This project was developed as a **college Python project** to understand basic Python programming concepts and GUI development.

---

## 📖 Introduction

Passwords are an important part of keeping personal accounts and information safe. However, creating a strong and random password manually can be difficult.

The **Random Password Generator** provides a simple solution to this problem. It allows the user to enter the desired password length and automatically generates a random password.

The project uses Python's built-in modules such as `random` and `string` to select characters randomly.

A simple graphical user interface is created using **Tkinter**, making the application easy to use.

---

## ✨ Features

- 🔐 Generates random passwords
- 🔢 Allows the user to enter password length
- 🔤 Uses uppercase and lowercase letters
- 🔢 Includes numbers
- 🔣 Includes special characters
- 📋 Allows the generated password to be copied
- ⚠️ Handles invalid input
- 🖥️ Simple graphical user interface
- 🐍 Beginner-friendly Python project

---

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| Python | Main programming language |
| Tkinter | Creating the graphical user interface |
| Random | Selecting random characters |
| String | Providing letters, numbers and special characters |

---

## 📂 Project Structure

## Flowchart

                 START
                   │
                   ▼
          Open the Application
                   │
                   ▼
          Enter Password Length
                   │
                   ▼
             Validate Input
                   │
             ┌─────┴─────┐
             │           │
          Invalid       Valid
             │           │
             ▼           ▼
        Show Error   Create Character Pool
                         │
                         ▼
                  Select Random
                   Characters
                         │
                         ▼
                  Generate Password
                         │
                         ▼
                  Display Password
                         │
                         ▼
                  Copy Password
                    (Optional)
                         │
                         ▼
                        END

## Workflow

             ┌───────────────┐
             │     START     │
             └───────┬───────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Enter Password      │
          │ Length              │
          └──────────┬──────────┘
                     │
                     ▼
          ┌─────────────────────┐
          │ Is Input Valid?     │
          └──────────┬──────────┘
                     │
                ┌────┴────┐
                │         │
               NO        YES
                │         │
                ▼         ▼
        ┌────────────┐  ┌──────────────────┐
        │ Show Error │  │ Create Character │
        │ Message    │  │ Pool             │
        └──────┬─────┘  └────────┬─────────┘
               │                 │
               │                 ▼
               │        ┌──────────────────┐
               │        │ Select Random    │
               │        │ Characters       │
               │        └────────┬─────────┘
               │                 │
               │                 ▼
               │        ┌──────────────────┐
               │        │ Generate         │
               │        │ Password         │
               │        └────────┬─────────┘
               │                 │
               │                 ▼
               │        ┌──────────────────┐
               │        │ Display Password │
               │        └────────┬─────────┘
               │                 │
               │                 ▼
               │        ┌──────────────────┐
               │        │ Copy Password    │
               │        │ (Optional)       │
               │        └────────┬─────────┘
               │                 │
               └────────┬────────┘
                        │
                        ▼
                ┌───────────────┐
                │      END      │
                └───────────────┘

