# Contracts for char_max_add

## x42.c

```
static char badSource(char data)
{
    /* POTENTIAL FLAW: Use the maximum size of the data type */
    data = CHAR_MAX;
    return data;
}
```
**postcondition**: return = MAXINT8

```
static char goodG2BSource(char data)
{
    /* FIX: Use a small, non-zero value that will not cause an overflow in the sinks */
    data = 2;
    return data;
}
```
**postcondition**: return = 2


## x45.c

```
static void badSink()
{
    char data = CWE190_Integer_Overflow__char_max_add_45_badData;
    {
        /* POTENTIAL FLAW: Adding 1 to data could cause an overflow */
        char result = data + 1;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_max_add_45_badData < MAXINT8

```
static void goodG2BSink()
{
    char data = CWE190_Integer_Overflow__char_max_add_45_goodG2BData;
    {
        /* POTENTIAL FLAW: Adding 1 to data could cause an overflow */
        char result = data + 1;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_max_add_45_goodG2BData < MAXINT8


## x61b.c

```
char CWE190_Integer_Overflow__char_max_add_61b_badSource(char data)
{
    /* POTENTIAL FLAW: Use the maximum size of the data type */
    data = CHAR_MAX;
    return data;
}
```
**postcondition**: return = MAXINT8

```
char CWE190_Integer_Overflow__char_max_add_61b_goodG2BSource(char data)
{
    /* FIX: Use a small, non-zero value that will not cause an overflow in the sinks */
    data = 2;
    return data;
}
```
**postcondition**: return = 2


## x68b.c

```
void CWE190_Integer_Overflow__char_max_add_68b_badSink()
{
    char data = CWE190_Integer_Overflow__char_max_add_68_badData;
    {
        /* POTENTIAL FLAW: Adding 1 to data could cause an overflow */
        char result = data + 1;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_max_add_68_badData < MAXINT8

```
void CWE190_Integer_Overflow__char_max_add_68b_goodG2BSink()
{
    char data = CWE190_Integer_Overflow__char_max_add_68_goodG2BData;
    {
        /* POTENTIAL FLAW: Adding 1 to data could cause an overflow */
        char result = data + 1;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_max_add_68_goodG2BData < MAXINT8
