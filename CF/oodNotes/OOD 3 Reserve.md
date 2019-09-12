
## Reserve
- search 
    - Base on search criteria
    - Go through rooms to check availability
    - List available room types and available count

- select (make reserviation)
    - add roomType, time, and number of rooms in a request
    - send request to hotal
    - if there is engouth room left, confirm the reservation
    - if there isn't enought room left, throw exception 
- cannal 


### restaurant
- ![restaurant](./assets/chap3_1.png)

- chanllge 
    - How to handler reservation?
        -  可以预定：直接进入Confirm阶段
        -  不能预定： Throw exception / Show message
         - Design:  Map<Timeslot, Set<Table>> findTableForReservation(Time slot) throws NoTableForReservationException
         - void confirmReservation( Reservation reservation)
         - void cannalReservation( Reservation reservation)
            - Reservation
                - Table table
                - Timeslot timeSlot

    - How to know if a table is open for reservation for a timeslot?
        - base on Timeslot, 比如一个timeSlot 是2小时。 一个客户预约2点#3桌子，然后timeSlot就说2-4点. 
            Map<Timeslot, Set<Table>>
                 2-4，       #3
        - 保存一个Centralized的Map, 有被confirm过的timeslot就插入这个Map.
            Map<Timeslot, Set<Table>>
            当query一个新的timeslot的时候，检查这个区间内已经被预定过的Table,
            排除之后剩下的就是可选的桌子，随意选一张即可

### Hotal

- Search room from one hotal by loaction and time?
    - Search criteria-> search() -> List<result> -> Select() -> Receipt
        - result should be room type
    - - ![Hotal](./assets/chap3_2.png)

- Search all hotal by loaction and time?
    - Search criteria-> search() -> List<result> -> Select() -> Receipt
        - result should be room type
    - ![Booking Hotal](./assets/chap3_2.png)