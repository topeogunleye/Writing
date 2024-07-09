## Part 1: Redis for Beginners (Part 1 of 2)

### Introduction

Redis has come a long way through an evolution and, by now, it can be placed as your primary database—not just a cache layer. It features added data persistence and replication for durability and availability. Additional modules for JSON support and search make it easier to store and query more complex data. Now, Redis has an Object mapping library, Redis OM, which simplifies things.

In this two-part series, the focus is on the core of Redis. This is the first part, which will guide you through setting up a Redis database and using some basic commands.

### Setting Up a Redis Database

#### On a Macbook, use Homebrew

First, make sure you have Homebrew installed. From the terminal, run:

```bash
brew --version
```

If this command fails, you'll need to follow the Homebrew installation instructions.

#### Installation

From the terminal, run:

```bash
brew install redis
```

This will install Redis on your system.

#### On a Windows, use WSL

Microsoft provides detailed instructions for installing WSL. Once you're running Ubuntu on Windows, you can follow the steps detailed at Redis Site Installation Steps which are the same steps for installing Redis on Linux to install recent stable versions of Redis from the official packages.

#### Using Redis Cloud

The last option for installing Redis is called Redis Cloud, and that's what you’ll be using here. It allows you to set up a Redis database online. It also comes with Redis insights that can be used to test different commands and visualize your stored data.

**To use the Redis database online, follow the steps below:**

1. **Sign Up for a Free Redis Account:**
   - Visit the Redis website (https://redis.io/) and sign up for a free account.
   - Provide the necessary details and create your account.

2. **Create a Subscription:**
   - Once logged in, navigate to the “Subscriptions” section (usually found in the left-hand menu).
   - Click on “New Database” or a similar option.
   - Scroll down and select the free tier, which typically comes with 30MB of storage.
   - Click on “Create Database.”

3. **Download the Redis App:**
   - To work with Redis locally, download the Redis app for your system (Windows, macOS, or Linux).
   - Install the app following the instructions provided.

4. **Connect to Your Database:**
   - After creating the database, find the “Connect” option and click on it.
   - Click on the "Open with RedisInsights" button. This will launch your installed Redis application.

### Basic Commands

When using your RedisInsights application, navigate to your workbench. You can access your workbench by clicking on this icon:

#### SET: Using the SET Command to Set a Key-Value Pair

To set a key-value pair in Redis, follow these steps:
1. In your workbench input section, type the following command:

```bash
SET key value
```

Replace `key` with the name of the key you want to set, and `value` with the corresponding value you want to assign to that key.

2. Press `CTRL + Enter` to execute the command. For example, executing `SET name maria` will set the value `"maria"` for the key `name`.

3. You should receive the message "OK" in the output section below, confirming that the key-value pair was successfully set.

4. To verify, go back to the Redis browser, switch to the data view, and refresh the view to see the updated key-value pair.

**Error Handling:**

If you include a space in your data without quotes, you’ll get a syntax error. To include spaces, enclose the data in quotes.

**Example:**
```bash
SET name "chun li"
```

#### GET: Retrieving a Value by Key

To retrieve the value of a specific key, use the GET command. In your workbench, type:

```bash
GET key
```

Replace `key` with the name of the key you want to retrieve. For example, if you have a key named `name` with the value "chun li", executing `GET name` will return "chun li". Press `CTRL + Enter` to execute the command.

#### DEL: Deleting Keys

To delete one or more keys and their associated values, use the `DEL` command. In your workbench, type:

```bash
DEL key1 key2 key3 ...
```

Replace `key1`, `key2`, `key3`, etc., with the names of the keys you want to delete. For example:

```bash
DEL name1 name2
```

Executing this command will delete the keys `name1` and `name2` along with their respective values. The command will return an integer indicating the number of keys deleted. For instance, a response of `2` indicates that two keys were successfully deleted. Press `CTRL + Enter` to execute the command.

#### SET MULTIPLE: Setting Multiple Key-Value Pairs

To set multiple key-value pairs simultaneously, use the `MSET` command. In your workbench, use:

```bash
MSET key1 value1 key2 value2 key3 value3
```

Replace `key1`, `key2`, `key3`, etc., with the names of the keys you want to set, and `value1`, `value2`, `value3`, etc., with their respective values. For instance:

```bash
MSET name1 maria name2 yoshi color green rating 10
```

This command sets the keys `name1`, `name2`, `color`, and `rating` with their respective values. Press `CTRL + Enter`. Ensure the key comes first, followed by the value.

#### GET MULTIPLE: Retrieving Multiple Values

To retrieve values for multiple keys at once, use the `MGET` command. In your workbench, use:

```bash
MGET key1 key2 key3
```

Replace `key1`, `key2`, `key3`, etc., with the names of the keys you want to retrieve. For example:

```bash
MGET name1 name2 rating
```

This command will return the values associated with keys `name1`, `name2`, and `rating`. Press `CTRL + Enter`. The values "maria", "Yoshi", and "10" will be returned in the output section.
#### GETRANGE: Retrieving Substrings

To retrieve a substring of the value of a key, use the `GETRANGE` command. In your workbench, use:

```bash
GETRANGE key start end
```

Replace `key` with the name of the key, `start` with the starting index, and `end` with the ending index. For example:

```bash
GETRANGE name 0 4
```

This command will return the substring of the value of `name` from index 0 to 4. If `name` has the value "chun li", the command will return "chun ".

### Conclusion of Part 1

In this first part of our Redis for Beginners series, you learned how to set up a Redis database and run basic commands such as setting, getting, deleting, and retrieving multiple key-value pairs. These are basic skills that anyone working with Redis should be conversant with.

In the next part of this series, we will explore more advanced commands, command options, and go into the differences between lists and sets in Redis. Stay tuned!


