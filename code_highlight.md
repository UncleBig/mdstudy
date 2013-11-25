## C code
---
edit your code here  
`
void * cal_consumer_thread(void * _id)
`


```hll
background-color
```
```c
comment
```
```err
Error
```
```k
keyword
```
```o
operator
```
```cp
Comment.Preproc
```
```gd
Generic.Deleted
```
```gr
Generic.Error
```
```gh
Generic.Heading
```
```gi
Generic.Inserted
```
```go
Generic.Output
```
```gs
Generic.Strong
```
```gu
Generic.Subheading
```
```gt
Generic.Traceback
```
```
d
```


```gs
void* cal_consumer_thread(void* _id) {
    long thread_id = (long)_id;
    u_int numCPU = sysconf( _SC_NPROCESSORS_ONLN );
    u_long core_id = thread_id % numCPU;
    int start, end;
    if ((num_cal_threads >1) && (numCPU > 1)) {
        if (bind2core(core_id) == 0)
            printf("Set cal thread %lu on core %lu/%u\n", thread_id, core_id, numCPU);
    }
    /*
     * NOTE: num_cal_threads should less than hash_table_size(/2)
     */
    start = (hash_table_size / num_cal_threads) * thread_id;
    end   = (hash_table_size / num_cal_threads) * (thread_id + 1);
    if ((thread_id + 1) == num_cal_threads)
        end += hash_table_size % num_cal_threads;

    while (1) {
       if(do_shutdown) break;
       /*
        * traverses the items associated with me every 1s
        */
    }
   return(NULL);
}
```