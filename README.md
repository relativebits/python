# python
Python tips and tricks


### Decorator to Calculator Method Execution Time
```
def timeit(method):
    def timed(*args, **kw):
        # start the timers
        perf_start = time.perf_counter()
        process_start = time.process_time()
        
        # execute the method
        method_result = method(*args, **kw)
        
        # stop the timers
        perf_end = time.perf_counter()
        process_end = time.process_time()
        
        # calculate speed
        perf_speed = perf_end - perf_start
        process_speed = process_end - process_start
        
        print('--------------------------------------------------')
        print(f'Elapsed time: {perf_speed} seconds')
        print(f'CPU process time: {process_speed} seconds')
        print('--------------------------------------------------')

        return method_result

    return timed
```    
    
