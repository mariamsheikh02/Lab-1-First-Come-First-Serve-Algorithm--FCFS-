# Lab-1-First-Come-First-Serve-Algorithm--FCFS-
class Process:

    def __init__(self, P_id, AT, BT):
        self.P_id = P_id
        self.AT = AT
        self.BT = BT
        self.CT = 0
        self.TAT = 0
        self.WT = 0

    def calculate(self):
        self.TAT = self.CT - self.AT
        self.WT = self.TAT - self.BT

    def get(self):
        print(
            f"P{self.P_id}\t{self.AT}\t{self.BT}\t{self.CT}\t{self.TAT}\t{self.WT}"
        )

    def turnaround(self):
        return self.TAT

    def waiting(self):
        return self.WT


n = int(input("Enter the Number of Processes: "))
processes = []

for i in range(n):
    print(f"\nProcess {i + 1}")
    AT = int(input("Enter Arrival Time: "))
    BT = int(input("Enter Burst Time: "))
    processes.append(Process(i + 1, AT, BT))

# Bubble Sort processes by Arrival Time
for i in range(n - 1):
    for j in range(n - i - 1):
        if processes[j].AT > processes[j + 1].AT:
            temp = processes[j]
            processes[j] = processes[j + 1]
            processes[j + 1] = temp

current_time = 0
for p in processes:
    if current_time < p.AT:
        current_time = p.AT
    current_time += p.BT
    p.CT = current_time
    p.calculate()

print("\nP_id\tAT\tBT\tCT\tTAT\tWT")
AVG_TAT = 0
AVG_WT = 0

for p in processes:
    p.get()
    AVG_TAT += p.turnaround()
    AVG_WT += p.waiting()

print(f"\nAverage Turnaround Time = {AVG_TAT / n:.2f}")
print(f"Average Waiting Time = {AVG_WT / n:.2f}")






# output
Enter the Number of Processes: 4

Process 1
Enter Arrival Time: 1
Enter Burst Time: 1

Process 2
Enter Arrival Time: 2
Enter Burst Time: 3

Process 3
Enter Arrival Time: 3
Enter Burst Time: 3

Process 4
Enter Arrival Time: 5
Enter Burst Time: 2

P_id	AT	BT	CT	TAT	WT
P1	1	1	2	1	0
P2	2	3	5	3	0
P3	3	3	8	5	2
P4	5	2	10	5	3

Average Turnaround Time = 3.50
Average Waiting Time = 1.25
