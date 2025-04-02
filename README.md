# Actividad de seguimiento - Simulación 1

|Integrante|correo|usuario github|
|---|---|---|
|Silvio Jose Otero Guzman|silvio.otero@udea.edu.co|silviootero|
|Gaia Ramirez Hincapie|gaia.ramirez@udea.edu.co|gaiamilenium99|

## Instrucciones

Antes de empezar a realizar esta actividad haga un **fork** de este repositorio y sobre este trabaje en la solución de las preguntas planteadas en la actividad de simulación. Las respuestas deben ser respondidas en español o si lo prefiere en ingles en el lugar señalado para ello (La palabra **answer** muestra donde).

**Importante**:
* Como la actividad es en las parejas del laboratorio, solo uno de los integrantes tiene que hacer el fork; y sobre repositorio bifurcado que se genera, la modificación se realiza en equipo.
* Como la entrega se debe hacer modificando el archivo READNE, se recomienda que consulte mas sobre el lenguaje **Markdown**. En el repo adjuntan dos cheatsheet ([cheat sheet 1](Markdown_Cheat_Sheet.pdf), [cheatsheet 2](markdown-cheatsheet.pdf)) para consulta rapida.
* Entre mas creativo mejor.

## Homework (Simulation)

This program, [`process-run.py`](process-run.py), allows you to see how process states change as programs run and either use the CPU (e.g., perform an add instruction) or do I/O (e.g., send a request to a disk and wait for it to complete). See the [README](https://github.com/remzi-arpacidusseau/ostep-homework/blob/master/cpu-intro/README.md) for details.

### Questions

1. Run `process-run.py` with the following flags: `-l 5:100,5:100`. What should the CPU utilization be (e.g., the percent of time the CPU is in use?) Why do you know this? Use the `-c` and `-p` flags to see if you were right.
   
   <details>
   <summary>Answer</summary>
   The percentage of CPU utilization is 100%, because it is executing two processes with 5 instructions and 100% of possibilities of executing them.
   </details>
   <br>
![Question 1](https://drive.google.com/uc?export=view&id=1YnH3guODguTy8rK87Yo6XsMMS50tRmS9)

2. Now run with these flags: `./process-run.py -l 4:100,1:0`. These flags specify one process with 4 instructions (all to use the CPU), and one that simply issues an I/O and waits for it to be done. How long does it take to complete both processes? Use `-c` and `-p` to find out if you were right. 
   
   <details>
   <summary>Answer</summary>
   To complete the CPU instructions took 6 time units, but with the I/O execution it took 11 time units to complete both of them. 
   </details>
   <br>
![Question 2](https://drive.google.com/uc?export=view&id=1I12RBRtRXDH6fy51qvHOZTy1f5XQ1NcU)

3. Switch the order of the processes: `-l 1:0,4:100`. What happens now? Does switching the order matter? Why? (As always, use `-c` and `-p` to see if you were right)
   
   <details>
   <summary>Answer</summary>
   Now the instructions can use the CPU while the I/O is blocked. Switching the order optimizes the execution.
   </details>
   <br>
![Question 3](https://drive.google.com/uc?export=view&id=13TOJquTzTM5T9MyJC9lx1JOYEKXhXjyt)

4. We'll now explore some of the other flags. One important flag is `-S`, which determines how the system reacts when a process issues an I/O. With the flag set to SWITCH ON END, the system will NOT switch to another process while one is doing I/O, instead waiting until the process is completely finished. What happens when you run the following two processes (`-l 1:0,4:100 -c -S SWITCH ON END`), one doing I/O and the other doing CPU work?
   
   <details>
   <summary>Answer</summary>
   This command prevents the system from switching to another process while one is doing I/O.
   </details>
   <br>
![Question 4](https://drive.google.com/uc?export=view&id=1skoM0uMW7ZApZ67pijTGa_nnLbfNk8dV)

5. Now, run the same processes, but with the switching behavior set to switch to another process whenever one is WAITING for I/O (`-l 1:0,4:100 -c -S SWITCH ON IO`). What happens now? Use `-c` and `-p` to confirm that you are right.
   
   <details>
   <summary>Answer</summary>
   This one allows to use both instructions an I/O call at the same time. This is a matter that can be evidenced in the execution time comparing this process with the previous one because that one took 11 time units and this one took 7 time units.
   </details>
   <br>
![Question 5](https://drive.google.com/uc?export=view&id=1skoM0uMW7ZApZ67pijTGa_nnLbfNk8dV)

6. One other important behavior is what to do when an I/O completes. With `-I IO RUN LATER`, when an I/O completes, the process that issued it is not necessarily run right away; rather, whatever was running at the time keeps running. What happens when you run this combination of processes? (`./process-run.py -l 3:0,5:100,5:100,5:100 -S SWITCH ON IO -c -p -I IO RUN LATER`) Are system resources being effectively utilized?
   
   <details>
   <summary>Answer</summary>
   When we run this combination of processes at the beginning the I/O is executed and the first CPU process is ready and waiting, then the first CPU process begins to execute while the I/O is blocked, then when it is done the next CPU process begins his execution, and then it carry on the execution of all the CPU processes while the O/I awaits. When all of then are done, the rest of I/O calls are executed. The conclusion is that the system resources aren't being efetively utilized, because when the I/O is blocked, the CPU is not being used.
   </details>
   <br>
![Question 6](https://drive.google.com/uc?export=view&id=1LXuWZ7qsRbaYbSr7PjjTcFacDE-IGeXy)

7. Now run the same processes, but with `-I IO RUN IMMEDIATE` set, which immediately runs the process that issued the I/O. How does this behavior differ? Why might running a process that just completed an I/O again be a good idea?
   
   <details>
   <summary>Answer</summary>
   When we used -I IO RUN IMMEDIATE, all the processes that issued the I/O are executed when they can, which leads to better ussage of the resources. It can be seen in the times, with the same command line this way it only took 21 time units while when it waits it took 31 time units.
   </details>
   <br>
![Question 7](https://drive.google.com/uc?export=view&id=1ufWjSggt3CBGijV2ylswkAZW4GKvPYRE)

### Criterios de evaluación
- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
