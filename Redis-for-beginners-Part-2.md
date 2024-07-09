## Part 2: Redis for Beginners (Part 2 of 2)

### Introduction

Welcome to the second part of our Redis for Beginners series. In the first part, we covered the basics of setting up a Redis database and executing fundamental commands. In this second part, we will explore advanced command options and delve into the differences between lists and sets in Redis.

### Command Options

Not all commands have options, but a few, for example SET, have certain added features that can be essential.

- **EX seconds**: Sets an expiration time in seconds (must be a positive integer).
- **PX milliseconds**: Sets an expiration time in milliseconds (must be a positive integer).
- **EXAT timestamp-seconds**: Sets a specific Unix timestamp for expiration (must be a positive integer).
- **NX**: Sets the key only if it does not already exist.
- **XX**: Sets the key only if it already exists.

You can't use NX and XX together because they will conflict with each other. Also, you can use only one option for expiration (EX or PX) at a time. To learn more about the SET command visit here to check out the Redis documentation page.

#### Example: SET Command Using the EX Option

When executing the following at your workbench, you will define a key with an expiration in Redis:

```bash
SET key value EX seconds
```

Replace `key` with the name of the key that contains the string and `value` with the new value you would like to store. Replace `seconds` with the amount of time, in seconds, after which the key should expire.

For example, if you have a key `name` currently holding the value "Mario", and you want to replace it with "Yoshi" after 7 seconds, run:

```bash
SET name Yoshi EX 7
```

This command updates the value of `name` to `"Yoshi"` and sets an expiration of 7 seconds from the time the command is executed.

#### Example: SET Command with NX and XX Options

You can set the key conditionally with respect to its existence in Redis by using the options NX, which stands for Not eXists, and XX, which stands for eXists, in the SET command:

**Using `NX` (Not eXists) Option:**

```bash
SET key value NX
```

- Replace `key` with the name of the key you want to set.
- Replace `value` with the value you want to store in the key.

This command sets the value of `key` to `value` only if `key` does not already exist. If `key` already exists, the command will not perform any action.

**Example:**

If you want to set a new key `username` to `"alice"` only if `username` does not already exist, you would use:

```bash
SET username alice NX
```

**Using `XX

` (eXists) Option:**

```bash
SET key value XX
```

This command sets the value of `key` to `value` only if `key` already exists. If `key` does not exist, the command will not perform any action.

**Example:**

If you want to update the value of an existing key `username` to `"bob"` only if `username` already exists, you would use:

```bash
SET username bob XX
```

### Lists vs. Sets

#### Lists

- An ordered collection of strings.
- Supports operations like adding elements to the head or tail, trimming based on ranges, etc.
- Useful for maintaining ordered data structures.
- Commands: `RPUSH`, `LPUSH`, `LRANGE`, `LPOP`, `RPOP`, etc.

#### Sets

- An unordered collection of unique strings.
- Supports operations like adding, removing, and checking membership.
- Useful for storing unique items and performing set operations.
- Commands: `SADD`, `SREM`, `SMEMBERS`, `SISMEMBER`, etc.

When deciding between lists and sets, consider the order requirements and the need for uniqueness in your data.

---

## Conclusion
Redis has come a long way through an evolution and, by now, it can be placed as your primary database—not just a cache layer. It features added data persistence and replication for durability and availability. Additional modules for JSON support and search make it easier to store and query more complex data. Now, Redis has an Object mapping library, Redis OM, which simplifies things. In this series, the focus is on the core of Redis.

