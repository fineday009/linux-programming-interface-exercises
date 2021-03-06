Chapter 08: Users and Groups
============================

Exercise 8-1
------------

**Question**

When we execute the following code, we find that it displays the same
number twice, even though two users have different IDs in the password
file.  Why is this?

    printf("%ld %ld\n", (long) (getpwnam("avr")->pw_uid),
                        (long) (getpwnam("tsr")->pw_uid));

**Answer**

getpwnam() is not reentrant.  That is, with both calls it returns a
refernce to the same statically allocated strcture in memory.  So,
only the result from the second call (for "tsr") will be present for
each.  If one had instead done the following, the expected results
should be provided:

    printf("%ld ", (long) (getpwnam("avr")->pw_uid));
    printf("%ld\n", (long) (getpwnam("tsr")->pw_uid));

Exercise 8-2
------------

**Question**

Implement getpwnam() using setpwent(), getpwent(), and endpwent().

**Answer**

See getpwnam.c.  Here's an example run of the test application:

```
$ ./prog_getpwnam posborne
struct passwd {
  pw_name="posborne",
  pw_uid=1000,
  pw_gid=1000,
  pw_dir="/home/posborne",
  pw_shell="/bin/bash"
}
```

