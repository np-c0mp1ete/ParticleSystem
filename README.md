﻿# ParticleSystem

Update of particles' positions happens in the separate thread in the ```WorkerThread``` function. For speeding up the particles proccesing the buffer is splitted in parts which are updated asynchroniously.

Для избежания зависимости между рендером и апдейтом используется тройная буферизация. В случае, когда рендер занимает много времени и оба остальных буфера успевают обновиться, то в качестве нового текущего берется более старый из них и просчет новых позиций происходит в него.

Синхронизация потоков необходима на время смены буферов и добавления/удаления новых эффектов.

Для хранения эффектов используется циклический буфер, так как он предотвращает переполнение, хранит элементы последовательно в памяти и обеспечивает быстрое удаление и добавление, так как элементы упорядочены по времени появления и имеют константную длительность жизни.

При реализации были изучены следующие статьи:

http://cowboyprogramming.com/2007/01/05/multithreading-particle-sytems/

https://software.intel.com/en-us/blogs/2011/02/18/building-a-highly-scalable-3d-particle-system
