---
{"dg-publish":true,"permalink":"/works/gantt-project-management-software-handbook/"}
---


# 总览
编写的 Gantt 项目管理软件，可以对 Excel 文件进行更新。本文档，即说明 Gantt 软件+Excel 文件的使用说明。
## Excel 文件结构说明
Excel 模版文件，包含三个 sheet，分别为：《GanttUpdateHistory》，《GanttChart》，《CalendarConfig》。

### 《GanttUpdateHistory》
该 sheet 用于记录 Gantt 计划的变更说明，方便回顾。该页内容由使用者根据实际情况填写。

### 《GanttChart》
该 sheet 是主要的记录跟踪页面，用于记录项目的进展。其中抬头部分：
1. 项目标题：用于说明该文件记录的项目，例如“XXX 项目实施进展”
2. 项目开始日期：填写项目开始的日期。日期格式为"YYYY-MM-DD"，例“2022-07-27”。Excel 本身会将该日期显示为“日期星期几”的格式，例如显示为“2022 年 7 月 27 日 Wednesday”。填写了项目开始日期后，右侧的甘特柱状图，会基于当前日期和开始日期，显示开始的周数和各周内的事项。


3. 项目经理：填写负责人名称 (可不填写)

GanttChat 表的主体部分，是一个统计表，其有如下列，分别做说明如下：
1. jobID：表示本任务的编号。jobID 推荐使用英文+数字的写法，例如"Job1","Job1.1","Job1.1a"，即为字符串 String 的类型。
> 不推荐采用纯数字的写法，因为任务 2.1 (第一个小任务) 会易被判定为和任务 2.10（第十个小任务）同一任务，造成误解。

2. Pre_jobID：表示本任务的前序任务。假如当前任务为 Job2.2，其为 Job2.1 完成后接的任务，即 Job2.2 的前序任务为 Job2.1。当前任务的开始时间 StartDate 会基于前序任务的完成时间进行更新：
> 当填写了当前任务的前序任务时，Gantt 软件会自动根据前序任务的完成时间，来更新当前任务的时间。即：
> 1. 当前序任务填写了实际完成时间 ActualDoneDate，程序会引用实际完成时间进行计算
> 2. 当前序任务无实际完成时间，但有计划完成时间 DueDate，程序会引用 DueDate 进行计算
> 3. 当前序任务没有 ActualDoneDate 和 DueDate 时，当前任务的开始时间不更新。
> 4. 当前任务的起始时间，从前序任务的完成时间更新过来。前序任务的写法，包括 “Job2.1”(表示前序任务完成时间，赋予当前任务的开始时间)；“Job2.1+1d”(表示前序任务完成时间，再推迟一天，赋予当前任务的开始时间。注意："+1d"紧接着"Job2.1 "写，中间不能有空格)；“Job2.1-1d”(表示前序任务完成时间的提前一天，赋予当前任务的开始时间)。同时关于时间的推算，Gantt 程序本身支持按照自然日和工作的区分计算。详见 [时间：自然日 day 和工作日 workday的区分](Gantt_Project-Management_Software_Handbook.md#时间：自然日%20day%20和工作日%20workday的区分)

3. PlanDays：表示当前任务从开始日期 (StartDate)，到计划完成日期 (DueDate) 所需的天数。支持自然日和工作日的模式。[时间：自然日 day 和工作日 workday的区分](Gantt_Project-Management_Software_Handbook.md#时间：自然日%20day%20和工作日%20workday的区分)
4. Stastus: 表示当前任务的状态，分为 Done (已完成) / Ongoing (进行中) / Watting (待开始) / Dued (已过期)。软件会根据当前的任务状态，自动更新。

5. Subject：表示当前任务所属的主题，手动填写。
6. job_Description：当前任务的描述，手动填写。
7. Team：该任务的执行团队，手动填写。
8. Owner：该任务的负责人
9. StartDate：任务开始日期。日期格式 follow [时间格式](Gantt_Project-Management_Software_Handbook.md#时间格式)
> StartDate 可自动更新。如无前级任务，则不更新当前的 StartDate。如果当前任务有填写了 Pre_jobID，则会根据前级任务时间进行更新：
> 1. 前级任务时间：当有 ActualDoneDate 时，取实际完成时间；如无实际完成时间，则取 DueDate。
> 2. 当前任务的开始时间 StartDate，可根据前级任务的时间更新。当前任务的开始时间，默认等于前级任务时间。也支持前级任务后的一定时间才开始，例如当前任务的前级任务为 Job7.13+2d，即表示 Job7.13 任务后的 2 天后才开始。该部分支持自然日和工作日的模式。
11. DueDate：任务**计划**结束日期。日期格式 follow [时间格式](Gantt_Project-Management_Software_Handbook.md#时间格式)
> 会根据 StartDate 和 PlanDays 更新 DueDate，即 StartDate+PlayDays=DueDate。
13. Note：任务的笔记
14. ActualDoneDate：任务的实际完成时间，手动填写任务完成时间。
15. MileStoneDate：如该任务做完 milestone，必须在这前完成的时间。

# 软件使用说明
软件打包成了 exe 程序，便于单机运行。
- 将软件和 Excel 文件，放在同一个文件夹中
- 双击 exe 程序，会跳出执行窗口
- 在执行窗口中，会要求输入 Excel 文件名称，包含后缀 (xlsx)
- 在执行窗口中，输入 Excel 是否打开的状态（1 或 0）
> 本软件支持 Excel 文件打开时进行更新；也支持在 Excel 文件关闭时进行更新。
> 输入 1 代表当前 Excel 为打开的状态，输入 0 代表当前 Excel 为关闭的状态。

- 软件会自动对 Excel 进行处理，包括：
	- 将当前 Excel 复制一份，文件尾贴上时间戳，放在当前路径的 Gantt_Backup 文件夹下
	- 对 Excel 文件进行更新。如果 Excel 为打开的状态，则会在打开的状态下进行更新，用户在屏幕上可以看到实时的更新。如果 Excel 为关闭的状态，则会直接对 Excel 进行更新。

- 当前程序跑完后，可在 Excel 中看到更新后的内容。
- 也可继续输入文件名，程序继续对文件进行更新。
# 其他
## 时间格式
日期的输入格式至关重要。正确的格式，能够使得内容被软件读取和计算。
> 本 Excel 内的日期格式，均必须为“YYYY-MM-DD”格式！

## 时间：自然日 day 和工作日 workday的区分
1. 日期时间的计算，支持“自然日 day”和“工作日 workday”模式。自然日的缩写为 d，工作日的缩写为 wd。工作日默认为周一到周五，不包含周六和周日。
- 即如果日期填写 7d，即表示从当前日期后的 7 个自然日。例如 2022-12-01 (周四) 后的 7d，为 2022-12-08。
- 即如果日期填写 7wd，即表示从当前日期后的 7 个工作日。例如 2022-12-01 (周四) 后的 7wd，为 2022-12-12 (周一)。即跳除了 2022-12-03 (周六), 2022-12-04 (周日)，2022-12-10 (周六), 2022-12-11 (周日)。

2. Workday 默认是周一~周五为工作日，周六日为休息日。可以自定义 workday 的日期。即定义那些日期是工作日，那些日期是休息日。在 Excel 的《CalendarConfig》里，可以填写相应日期。日期格式 follow [时间格式](Gantt_Project-Management_Software_Handbook.md#时间格式)
- Weekday_not_Work 列，填写周一~周五但是休息的日期。例如五一，十一放假的时间如在周一~周五，可填写进来。
- Weekend_still_Work 列，填写周六日仍工作的日期。例如五一，十一后的加班时间如在周六日，可填写进来。

