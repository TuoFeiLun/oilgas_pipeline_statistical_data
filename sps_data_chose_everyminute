import csv
from datetime import datetime , timedelta
from pprint import pprint
import timeit

def read_csv_file(filepath):
    csv_list = []
    with open(filepath, newline='') as csvfile:
        spamreader = csv.reader(csvfile, delimiter=' ', quotechar='|')
        for row in spamreader:
            after_split = row[1].split(',')
            after_split.insert(0, row[0])
            csv_list.append(after_split)
    return csv_list

def str2datetime(ds , ts):
    alldatetime  = ds+ts
    dt = datetime.strptime(alldatetime,  "%Y/%m/%d%H:%M:%S")
    return dt
def integerminutelist(starttime, endtime):
    # 生成一个整数分钟的列表
    days =  endtime.day  - starttime.day
    if days < 0:
        return 0
    dt = timedelta(minutes=1)
    a_list = []

    allminutes = days*60*24
    print('allminutes = ',allminutes )
    add_time = starttime
    for i in range(allminutes):
        add_time = add_time + dt
        a_list.append(add_time)
    return a_list

def csv_file_add_datetime(csv_list):
    for i in range(1, len(csv_list)):
        datetime   = str2datetime(csv_list[i][0],csv_list[i][1])
        csv_list[i].append(datetime) # 添加在了末尾 [5]

    return csv_list

def match_integer_time(csvtimefile : list , integertimelist: list ) -> list :
    interger_list = list(range(len(integertimelist)-1))  # 删除最后一个时刻
    for i in range(len(integertimelist)):
        onetime = integertimelist[i]
        delmaxseconds = timedelta.max
        for j in range(1,len(csvtimefile)):
            newcsvlist = csvtimefile[j][5]
            # if onetime.day == newcsvlist.day and onetime.hour == newcsvlist.hour and onetime.minute == newcsvlist.minute:
            #     interger_list.append(csvtimefile[j])
            #     break
            if onetime.day == newcsvlist.day and onetime.hour == newcsvlist.hour:
                des = abs(onetime- newcsvlist)
                if des < delmaxseconds:
                    delmaxseconds = des
                    interger_list[i] = csvtimefile[j]

    return interger_list

def csvwrite2file(filepath,alllist):
    with open(filepath, 'w', newline='') as csvfile:
        spamwriter = csv.writer(csvfile, delimiter=',',
                                quotechar='|', quoting=csv.QUOTE_MINIMAL)
        for one in alllist[::-1]:  # 时间倒序排列
            spamwriter.writerow(one)

if __name__ == '__main__':
    start = timeit.default_timer()

    # Your statements here


    filepath = r"C"
    savepath = r"+1.csv"

    c = read_csv_file(filepath)

    new_add  = csv_file_add_datetime(c)
    print(len(new_add))
    d = '2019/8/27'
    t = '00:00:00'
    d1 = '2019/8/30'
    t1 = '00:00:00'
    s1 = str2datetime(d,t)
    s2 = str2datetime(d1, t1 )

    l1 = integerminutelist(s1 , s2)
    print(len(l1))
    m = match_integer_time(new_add , l1 )
    pprint(m)
    print(len(m))
    csvwrite2file(savepath,m)
    stop = timeit.default_timer()

    print('Time: ', stop - start)
