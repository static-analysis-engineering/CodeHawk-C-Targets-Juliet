# Contracts for char_max_square

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


# x45.c

```
static void badSink()
{
    char data = CWE190_Integer_Overflow__char_max_square_45_badData;
    {
        /* POTENTIAL FLAW: if (data*data) > CHAR_MAX, this will overflow */
        char result = data * data;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_max_square_45_badData *
CWE190_Integer_Overflow__char_max_square_45_badData <= MAXINT8

```
static void goodG2BSink()
{
    char data = CWE190_Integer_Overflow__char_max_square_45_goodG2BData;
    {
        /* POTENTIAL FLAW: if (data*data) > CHAR_MAX, this will overflow */
        char result = data * data;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_max_square_45_goodG2BData; *
CWE190_Integer_Overflow__char_max_square_45_goodG2BData; <= MAXINT8


# x61b.c

```
char CWE190_Integer_Overflow__char_max_square_61b_badSource(char data)
{
    /* POTENTIAL FLAW: Use the maximum size of the data type */
    data = CHAR_MAX;
    return data;
}
```
**postcondition**: return = MAXINT8

```
char CWE190_Integer_Overflow__char_max_square_61b_goodG2BSource(char data)
{
    /* FIX: Use a small, non-zero value that will not cause an overflow in the sinks */
    data = 2;
    return data;
}
```
**postcondition**: return = 2


# x68b.c

```
void CWE190_Integer_Overflow__char_max_square_68b_badSink()
{
    char data = CWE190_Integer_Overflow__char_max_square_68_badData;
    {
        /* POTENTIAL FLAW: if (data*data) > CHAR_MAX, this will overflow */
        char result = data * data;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_max_square_68_badData *
CWE190_Integer_Overflow__char_max_square_68_badData  <= MAXINT8


```
void CWE190_Integer_Overflow__char_max_square_68b_goodG2BSink()
{
    char data = CWE190_Integer_Overflow__char_max_square_68_goodG2BData;
    {
        /* POTENTIAL FLAW: if (data*data) > CHAR_MAX, this will overflow */
        char result = data * data;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_max_square_68_goodG2BData *
CWE190_Integer_Overflow__char_max_square_68_goodG2BData <= MAXINT8
