# OEE Metrics
Let's explain the calculation with a sample data shown below:


Machine Status Timeline:

| S.No | Machine Name | Start Time          | End Time            | Duration | Machine State | Label        | Label Value     | Rejected Part |
|------|--------------|---------------------|---------------------|----------|---------------|--------------|-----------------|---------------|
| 1.   | MCV - 450    | 31-05-2023T11:15:03 | 31-05-2023T11:17:09 | 126      | production    | program name | crank_feature_1 | no            |
| 2.   | MCV - 450    | 31-05-2023T11:17:09 | 31-05-2023T11:17:45 | 36       | idle          | reason       | part_change     | nil           |
| 3.   | MCV - 450    | 31-05-2023T11:17:45 | 31-05-2023T11:19:22 | 127      | production    | program name | crank_feature_1 | no            |


Planned Event Timeline:

| S.No | Date       | Shift | Start Time         | End Time           | Duration (s) |
|------|------------|-------|--------------------|--------------------|--------------|
| 1.   | 31/05/2023 | 1     | 31-05-2023T8:00:00 | 31-05-2023T4:00:00 | 28800        |

Part Program Meta Data:

| S.No | Machine Name | Program Name    | Ideal Cycle Time (s) |
|------|--------------|-----------------|----------------------|
| 1.   | MCV - 450    | crank_feature_1 | 120                  |

## Availability

The formula for availability is given by:

$$
\text{Availability} = \frac{\text{Actual Production Time}}{\text{Planned Production Time}}
$$


Let's say we want to find the availability between 

Start time : 31-05-2023T11:15:03 

End time: 31-05-2023T11:19:22

1. Find the planned production time for the given duration:
    
    1. We can see that from the planned event timeline, the query start and end datetime falls under prodution (full time), hence the planned production time for the given query time duration is the query time duration itself (which is 31-05-2023T11:19:22 - 31-05-2023T11:15:03 = 289 s).

    $$
    \text{Planned Production Time} = \text{289}
    $$

2. Find the Actual Production Time:
    
    1. The actual production time is given by summation of duration column in the Machine Status Timeline table for all rows where the machine state column has value production.
    2. For example in the current case: 126 + 127 = 253 seconds.

    $$
    \text{Actual Production Time} = \text{253}
    $$

3. Find Availability:
    
    1. By substituting in the previous formula we can find the value

    $$
    \text{Availability} = \frac{\text{253}}{\text{289}}
    $$

    $$
    \text{Availability} = {\text{0.8754}}
    $$

    $$
    \text{Availability \%} = {\text{87.54 \%}}
    $$

## Performance

The formula for Performance is given by:

$$
\text{Performance} = \frac{\text{Ideal Production Time}}{\text{Actual Production Time}}
$$

1. Find Ideal Production Time:
    
    1. The ideal production time is determined by summing up the ideal cycle times for all the cycles that occurred between the given start and end time. To calculate this, we require information from two tables. First, we utilize the machine status time line table, which provides the start and end times of all the cycles that took place within the specified query start and end time, along with the corresponding part program name for each cycle. Secondly, we need to access the Part Program Meta Data table to obtain the ideal cycle time associated with each part program name. Once we have this information, we can add up the ideal cycle times to obtain the ideal production time. It is important to note that performing a SQL join operation on these two tables is necessary to accomplish this calculation.

        $$
        \text{Ideal Production Time} = \sum \text{Ideal Cycle Times for All Cycles during the given Query Range}
        $$

    2. For example in the previous case, the following table gives all the production cycles along with the part program name

        1. Machine Status Timeline:

            | S.no | Machine Name | Start Time          | End Time            | Duration | Machine State | Label        | Label Value     |
            |------|--------------|---------------------|---------------------|----------|---------------|--------------|-----------------|
            | 1.   | MCV - 450    | 31-05-2023T11:15:03 | 31-05-2023T11:17:09 | 126      | production    | program name | crank_feature_1 |
            | 3.   | MCV - 450    | 31-05-2023T11:17:45 | 31-05-2023T11:19:22 | 127      | production    | program name | crank_feature_1 |

        2. The corresponding part program name is given below:

            Part Program Meta Data:

            | S.No | Machine Name | Program Name    | Ideal Cycle Time (s) |
            |------|--------------|-----------------|----------------------|
            | 1.   | MCV - 450    | crank_feature_1 | 120                  |
        
        3. Hence the sum would be 120 + 120 = 240

        $$
        \text{Ideal Production Time } = {\text{240}}
        $$

2. Sometime the ideal part program cycle time would not be available, it is the end user / developers responsibility to somehow update the values (Such as in cmti, it is not available, since we don't usually use cam softwares here.)
    1. One possible strategy is to update the part program's ideal cycle time to be equal to the minimum value of the set of cycle times (from the machine status timeline table, from duration column, when the machine state is production), at least this will ensure that we're comparing the cycle time to the lowest that was achieved by the machine.

2. The actual production time is already found in previous metric(Availability):

3. Find Performance

    $$
    \text{Performance} = \frac{\text{Ideal Production Time}}{\text{Actual Production Time}}
    $$

    $$
    \text{Performance} = \frac{\text{240}}{\text{253}}
    $$

    $$
    \text{Performance} = {\text{0.9486}}
    $$

    $$
    \text{Performance \%} = {\text{94.86 \%}}
    $$



## Quality

The formula for Quality is given by 

$$
\text{Quality} = \frac{\text{Good Parts Produced}}{\text{Total Parts Produced}}
$$

1. Total Parts:
    This can be calculated by querying the table of machine status timeline, the total count equal to the number of rows with column 'Machine State' equal to production and 
    
2. The number of good parts is equal to the number of rows where the rejected is not equal to 'No'.

3. For example in the above case 

    $$
    \text{Quality} = \frac{\text{2}}{\text{2}}
    $$

    $$
    \text{Quality } = {\text{1}}
    $$

    $$
    \text{Quality \%} = {\text{100 \%}}
    $$

## Overall Equipment Effectiveness (OEE)

The formula for OEE is given by 

$$
\text{OEE} = {\text{Availability}}\times{\text{Performance}}\times{\text{Quality}}
$$

$$
\text{OEE} = {\text{0.8754}}\times{\text{0.9486}}\times{\text{1}}
$$

$$
\text{OEE} = {\text{0.8304}}
$$

$$
\text{OEE \%} = {\text{83.04 \%}}
$$

# Six Big Losses
The Six Big Losses are a key concept in Total Productive Maintenance (TPM) and Overall Equipment Effectiveness (OEE). They represent the most common causes of efficiency loss in manufacturing. Here they are:

1. **Downtime Loss (Mapped to Availability in OEE)** 
    - **Breakdowns:** These are instances of equipment failure that result in unscheduled downtime. They can be caused by tooling failures, unplanned maintenance, equipment breakdown, etc.
    - **Setup and Adjustments:** This refers to the time taken to change over from one product variant to another. It includes setup and adjustment time during which the equipment is not operational.
    - **Idling and Small Stops:** These are minor stops or pauses in the production process that are usually less than 5 minutes and do not require maintenance personnel. They can be caused by issues like a blocked sensor or a minor jam.

2. **Speed Loss (Mapped to Performance in OEE)**
    - **Reduced Speed:** This refers to instances where the machinery is operating, but not at its optimal speed. This could be due to wear and tear, equipment issues, or sub-optimal operating conditions.

3. **Defect Loss (Mapped to Quality in OEE)**
    - **Startup Rejects:** These are defects that occur during the startup phase of production. When equipment is first started, it may take a while for it to operate correctly, resulting in defective output.
    - **Production Rejects:** These are defects that occur during steady-state production. Despite the equipment running as expected, there can still be quality losses due to factors like tool wear or process variation.
        - **Rework:** These are defects that can be rectified by some rework.
        - **Scrap:** These are defects that cannot be rectified and are scraped.

By identifying and targeting these Six Big Losses, manufacturers can significantly improve their OEE and overall productivity.
