# <img src="https://user-images.githubusercontent.com/2356749/235068474-5daddf05-54d6-4391-ae97-1a944aebdec6.png" style="height: 32px"> Google Bard CLI

A simple command line interface for interacting with Google Bard, written in Rust.

This CLI allows you to save chat history as a Markdown file at a specified absolute or relative path in realtime

and handles graceful exit with Ctrl+C.

## Prerequisites

You need to have Rust and Cargo installed on your system. If you don't have them, you can install them from the [official Rust website](https://www.rust-lang.org/tools/install).

## Installation

1. Clone the repository to your local machine:

   ```
   git clone https://github.com/tuhailong/bard
   ```

2. Change the working directory:

   ```
   cd bard
   ```

3. Build the project:

   ```
   cargo build --release
   ```

The executable binary file will be located in the `target/release` folder.

## Usage

Before using the Google Bard CLI, you need to obtain your session cookie. To get the session cookie, follow these steps:

1. Go to [Google Bard](https://bard.google.com/) in Chrome.
2. Open Chrome Developer Tools (F12 or `Ctrl + Shift + I`).
3. Go to the "Application" tab.
4. Under "Storage" > "Cookies", click on "https://bard.google.com".
5. Find the cookie with the name `__Secure-1PSID`, and copy its value. (it includes "." usually)

Now you can use the Google Bard CLI:

It'll save as your first prompt message. (eg: "Hey yo" -> bard_hey_yo.md)

```
bard --session <your_session_cookie> --path ./
```

Replace `<your_session_cookie>` with the value you copied from the Developer Tools.

If you don't want to save the chat history as a Markdown file, skip `--path`:

```
bard --session <your_session_cookie>
```

If you don't want to pass that long session in terminal, use `.env` file

```
bard -e .env -p ./
```

If you prefer not to specify a path, `bard` will automatically search for the .env file in the following locations: the argument-provided path, the current working directory, and the directory of the bard binary.

(`-p` is still required if you want to save the chat history as markdown file.)

```
bard
```

above command is same as `bard -e .env`

`.env` file must contain `BARD_SESSION_ID` key. (the keys being used for the `-s` value and `BARD_SESSION_ID` are identical, they are both derived from `__Secure-1PSID`)

> ! using `echo BARD_SESSION_ID=... > .env` might cause encoding problem that `dotenv` cannot read and end up causing no session key error.

```
BARD_SESSION_ID=~.
```

## Commands

- Type your message and press Enter to send it to Google Bard.
- Type `!reset` to reset the conversation.
- Type `!exit` to exit the CLI.

## License

This project is licensed under the [MIT License](LICENSE).

