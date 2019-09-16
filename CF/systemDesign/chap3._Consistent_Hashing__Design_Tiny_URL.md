#
- ![InConsistent Hashing](./assets/chap1_21.png)
- ![Consistent Hashing](./assets/chap1_22.png)
    - 缺陷1 数据分布不均匀 因为算法是“将数据最多的相邻两台机器均匀分为三台” 比如，3台机器变4台机器时，无法做到4台机器均匀分布
    - 新机器的数据只从两台老机器上获取 导致这两台老机器负载过大

- ![Squential ID Auto-increment](./assets/chap1_20.png)
    - 自增就必须加锁，会导致很慢
    - 不安全