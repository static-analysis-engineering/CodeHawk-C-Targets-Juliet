# Contracts for int64_t_fscanf_multiply

## x42.c

```
static int64_t badSource(int64_t data)
{
    /* POTENTIAL FLAW: Use a value input from the console */
    fscanf (stdin, "%" SCNd64, &data);
    return data;
}
```
**postconditions**: (tainted lb=MININT64 ub=MAXINT64)(return)

```
static int64_t goodG2BSource(int64_t data)
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
    int64_t data = CWE190_Integer_Overflow__int64_t_fscanf_multiply_45_badData;
    if(data > 0) /* ensure we won't have an underflow */
    {
        /* POTENTIAL FLAW: if (data*2) > LLONG_MAX, this will overflow */
        int64_t result = data * 2;
        printLongLongLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__int64_t_fscanf_multiply_45_badData * 2 <= MAXINT64

```
static void goodG2BSink()
{
    int64_t data = CWE190_Integer_Overflow__int64_t_fscanf_multiply_45_goodG2BData;
    if(data > 0) /* ensure we won't have an underflow */
    {
        /* POTENTIAL FLAW: if (data*2) > LLONG_MAX, this will overflow */
        int64_t result = data * 2;
        printLongLongLine(result);
    }
}
```
**precondition**: CWE190_Integer_Overflow__int64_t_fscanf_multiply_45_goodG2BData * 2 <= MAXINT64


## x61b.c

```
int64_t CWE190_Integer_Overflow__int64_t_fscanf_multiply_61b_badSource(int64_t data)
{
    /* POTENTIAL FLAW: Use a value input from the console */
    fscanf (stdin, "%" SCNd64, &data);
    return data;
}
```
**postcondition**: (tainted lb=MININT64 ub=MAXINT64)(return)

```
int64_t CWE190_Integer_Overflow__int64_t_fscanf_multiply_61b_goodG2BSource(int64_t data)
{
    /* FIX: Use a small, non-zero value that will not cause an overflow in the sinks */
    data = 2;
    return data;
}
```
**postcondition**: return = 2


## x68b.c

```
void CWE190_Integer_Overflow__int64_t_fscanf_multiply_68b_badSink()
{
    int64_t data = CWE190_Integer_Overflow__int64_t_fscanf_multiply_68_badData;
    if(data > 0) /* ensure we won't have an underflow */
    {
        /* POTENTIAL FLAW: if (data*2) > LLONG_MAX, this will overflow */
        int64_t result = data * 2;
        printLongLongLine(result);
    }
}
```
**preconditions**: CWE190_Integer_Overflow__int64_t_fscanf_multiply_68_badData * 2 <= MAXINT64

```
void CWE190_Integer_Overflow__int64_t_fscanf_multiply_68b_goodG2BSink()
{
    int64_t data = CWE190_Integer_Overflow__int64_t_fscanf_multiply_68_goodG2BData;
    if(data > 0) /* ensure we won't have an underflow */
    {
        /* POTENTIAL FLAW: if (data*2) > LLONG_MAX, this will overflow */
        int64_t result = data * 2;
        printLongLongLine(result);
    }
}
```
**preconditions**: CWE190_Integer_Overflow__int64_t_fscanf_multiply_68_goodG2BData * 2 <= MAXINT64

