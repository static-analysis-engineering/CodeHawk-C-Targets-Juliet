# Contracts for char_fscanf_multiply

## x42.c

```
static char badSource(char data)
{
    /* POTENTIAL FLAW: Use a value input from the console */
    fscanf (stdin, "%c", &data);
    return data;
}
```
**postcondition**: (tainted lb=MININT8 ub=MAXINT)(return)

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
    char data = CWE190_Integer_Overflow__char_fscanf_multiply_45_badData;
    if(data > 0) /* ensure we won't have an underflow */
    {
        /* POTENTIAL FLAW: if (data*2) > CHAR_MAX, this will overflow */
        char result = data * 2;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_fscanf_multiply_45_badData * 2 <= MAXINT8

```
static void goodG2BSink()
{
    char data = CWE190_Integer_Overflow__char_fscanf_multiply_45_goodG2BData;
    if(data > 0) /* ensure we won't have an underflow */
    {
        /* POTENTIAL FLAW: if (data*2) > CHAR_MAX, this will overflow */
        char result = data * 2;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_fscanf_multiply_45_goodG2BData * 2 <= MAXINT8


## x61b.c

```
char CWE190_Integer_Overflow__char_fscanf_multiply_61b_badSource(char data)
{
    /* POTENTIAL FLAW: Use a value input from the console */
    fscanf (stdin, "%c", &data);
    return data;
}
```
**postcondition**: (tainted lb=MININT8 ub=MAXINT8)(return)

```
char CWE190_Integer_Overflow__char_fscanf_multiply_61b_goodG2BSource(char data)
{
    /* FIX: Use a small, non-zero value that will not cause an overflow in the sinks */
    data = 2;
    return data;
}
```
**postcondition**: return = 2


## x68b.c

```
void CWE190_Integer_Overflow__char_fscanf_multiply_68b_badSink()
{
    char data = CWE190_Integer_Overflow__char_fscanf_multiply_68_badData;
    if(data > 0) /* ensure we won't have an underflow */
    {
        /* POTENTIAL FLAW: if (data*2) > CHAR_MAX, this will overflow */
        char result = data * 2;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_fscanf_multiply_68_badData * 2 <= MAXINT8

```
void CWE190_Integer_Overflow__char_fscanf_multiply_68b_goodG2BSink()
{
    char data = CWE190_Integer_Overflow__char_fscanf_multiply_68_goodG2BData;
    if(data > 0) /* ensure we won't have an underflow */
    {
        /* POTENTIAL FLAW: if (data*2) > CHAR_MAX, this will overflow */
        char result = data * 2;
        printHexCharLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__char_fscanf_multiply_68_goodG2BData * 2 <= MAXINT8
