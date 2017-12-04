### Openpyxl - deal Excel file with python

Tags: Tutorial 

---

Openpyxl-website --- > [https://openpyxl.readthedocs.io/en/default/index.html](https://openpyxl.readthedocs.io/en/default/index.html)


#####Create a workbook

There is no need to create a file on the filesystem to get started with openpyxl. Just import the Workbook class and start using it
	
	>>> import openpyxl
	>>> wb = openpyxl.Workbook()
	# or
	>>> from openpyxl import Workbook
	>>> wb = Workbook()
	
A workbook is always created with at least one worksheet. You can get it by using the openpyxl.workbook.Workbook.active() property

	>>> ws = wb.active
	
You can also create new worksheets by using the openpyxl.workbook.Workbook.create_sheet() method

	>>> ws1 = wb.create_sheet("Mysheet") # insert at the end (default)
	# or
	>>> ws2 = wb.create_sheet("Mysheet", 0) # insert at first position
	


#### a simple project 

	from openpyxl import load_workbook
	from openpyxl import Workbook
	import re
	
	# /User/xing/venPython/Example/2016-17.xlsx
	wb = load_workbook('2016-17.xlsx')
	
	# create a sheet-course_a to store the result
	ws_sta = wb.create_sheet('course_a')
	nL = wb.get_sheet_names()
	
	print nL
	# print type(wb)
	# print dir(wb)
	
	# print type(ws)
	# print dir(ws) 
	for i in nL:
	#     print i.encode('utf-8')
	    print i
	
	

	
	ws1 = wb.get_sheet_by_name(u'2015级 -学院组合')
	ws2 = wb.get_sheet_by_name(u'公选课')
	
	data = {}
	
	from types import *
	def dict_print(dic):
	    print '===' * 10
	    for key, value in dic.iteritems():
	        print key,
	        if type(value) is ListType:
	            for i in value:
	                print i, 
	        else:
	            print value
	        print '\n'
	    
	
	# print 'H{}'.format(3)
	for row in range(3, 164):
	    name = ws1['H{}'.format(row)].value.encode('utf-8')
	    level = ws1['E{}'.format(row)].value.encode('utf-8')
	    courses = ws1['I{}'.format(row)].value.encode('utf-8')
	    if name in data:
	#         print type(data[name])
	#         print  type(data[name])
	#         print type(data.get(name)[level])
	        if level in data.get(name):
	            data.get(name)[level].append(courses)
	        else:
	            data.get(name)[level] = [courses]
	            dict_print(data.get(name))
	    else:
	        data[name] = {level: [courses]}
	
	print '\n'        
	    
	# for key, value in data.iteritems():
	#     print key
	#     for lkey, lvalue in value.iteritems():
	#         print lkey,
	#         for i in lvalue:
	#             print i, 
	
	#     print '\n'
	    
	# print data
	
	# ====================================================
	# ==================== 公选课 =========================
	# ====================================================
	
	for row in range(3, 38):
	    name = ws2['H{}'.format(row)].value.encode('utf-8')
	    level = ws2['C{}'.format(row)].value.encode('utf-8')
	    courses = ws2['J{}'.format(row)].value.encode('utf-8')
	    if name in data:
	#         print type(data[name])
	#         print  type(data[name])
	#         print type(data.get(name)[level])
	        if level in data.get(name):
	            data.get(name)[level].append(courses)
	        else:
	            data.get(name)[level] = [courses]
	            dict_print(data.get(name))
	    else:
	        data[name] = {level: [courses]}
	
	print '\n'        
	    
	for key, value in data.iteritems():
	    print key
	    for lkey, lvalue in value.iteritems():
	        print lkey,
	        for i in lvalue:
	            print i, 
	
	    print '\n'
	    
	print data
	
	
	
	# =========================================
	# ======paly with data in excel file=======
	# =========================================
	
	def course_accout(li):
	    s = '\n'.join(li)
	    courc_a = len(re.findall(r'\d+', s))
	    # use list(set(t)) to remove the duplicates item
	    # check if there is duplicates item
	    if len(s.split('\n')) != len(set(s.split('\n'))):
	        print '===' * 20
	        print '===' * 9 + 'Not match' + '===' * 9
	        print '===' * 20
	    return courc_a
	
	
	def assign_A(lvalue, row, lkey='大学英语（2）A level'):
	    lv_c = '\n'.join(lvalue)
	    ws_sta['B' + str(row)].value = lv_c
	    # get the acources amount and then assign it right after the lv_c
	    courc_a = course_accout(lvalue)
	    ws_sta['C' + str(row)].value = courc_a
	
	def assign_B(lvalue, row, lkey='大学英语（2）B level'):
	    lv_c = '\n'.join(lvalue)
	    ws_sta['D' + str(row)].value = lv_c
	    courc_a = course_accout(lvalue)
	    ws_sta['E' + str(row)].value = courc_a
	
	def assign_C(lvalue, row, lkey='C level'):
	    lv_c = '\n'.join(lvalue)
	    ws_sta['F' + str(row)].value = lv_c
	    courc_a = course_accout(lvalue)
	    ws_sta['G' + str(row)].value = courc_a
	
	def assign_D(lvalue, row, lkey='D level'):
	    lv_c = '\n'.join(lvalue)
	    ws_sta['H' + str(row)].value = lv_c
	    courc_a = course_accout(lvalue)
	    ws_sta['I' + str(row)].value = courc_a
	      
	
	# ws_sta = wb.get_sheet_by_name('StatisticsSheet')
	
	row = 1
	col = 1
	for key, value in data.iteritems():
	#     print type(key)
	#     print key
	    ws_sta.cell(row=row, column=col).value = key
	    # lkey present the key of the layer of level
	    print '===' * 10
	    print row
	    for lkey in value.keys():
	        print value.keys(), len(value.keys())
	        if lkey == '大学英语（2）A level':
	            print 'A:  ', value[lkey]
	            assign_A(value[lkey], row)
	
	        elif lkey == '大学英语（2）B level':
	            print 'B:  ', value[lkey]
	            assign_B(value[lkey], row)
	
	        elif lkey == '雅思英语口语' or lkey == '大学英语(艺体类)（2）' or lkey == '雅思英语写作':
	            print 'C:  ', value[lkey]
	            assign_C(value[lkey], row)
	
	        else:
	            print 'D:  ', value[lkey]
	            assign_D(value[lkey], row)  
	    row += 1
	    print '\n'
	
	
	wb.save('First.xlsx')