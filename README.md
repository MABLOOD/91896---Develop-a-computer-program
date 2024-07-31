# 91896---Develop-a-computer-program
########################################################################
###This program is so we know julies party store ###
########################################################################

#import tkinter so we can make a GUI
from tkinter import *

#quit subroutine
def quit():
    main_window.destroy()

#print details of julies party store 
def print_camp_details ():
    name_count = 0
    #Create the column headings
    Label(main_window, font=("Helvetica 10 bold"),text="Row").grid(column=0,row=7)
    Label(main_window, font=("Helvetica 10 bold"),text="first_name").grid(column=1,row=7)
    Label(main_window, font=("Helvetica 10 bold"),text="last_name").grid(column=2,row=7)
    Label(main_window, font=("Helvetica 10 bold"),text="receipt_number").grid(column=3,row=7)
    Label(main_window, font=("Helvetica 10 bold"),text="amount").grid(column=4,row=7)
    #add each item in the list into its own row
    while name_count < counters['total_entries'] :
        Label(main_window, text=name_count).grid(column=0,row=name_count+8) 
        Label(main_window, text=(party_store_details[name_count][0])).grid(column=1,row=name_count+8)
        Label(main_window, text=(party_store_details[name_count][1])).grid(column=2,row=name_count+8)
        Label(main_window, text=(party_store_details[name_count][2])).grid(column=3,row=name_count+8)
        Label(main_window, text=(party_store_details[name_count][3])).grid(column=4,row=name_count+8)
        name_count +=  1

        counters['name_count'] = name_count
        
#Check the inputs are all valid
def check_inputs ():
    input_check = 0
    Label(main_window, text="               ") .grid(column=2,row=0)
    Label(main_window, text="               ") .grid(column=2,row=1)
    Label(main_window, text="               ") .grid(column=2,row=2)
    Label(main_window, text="               ") .grid(column=2,row=3)
    #Check that first name is not blank, set error text if blank   
    if len(entry_first_name.get()) == 0 :
        Label(main_window,fg="red", text="Required") .grid(column=2,row=0)
        input_check = 1
    #Check that last name is not blank, set error text if blank     
    if len(entry_last_name.get()) == 0 :
        Label(main_window,fg="red", text="Required") .grid(column=2,row=1)
        input_check = 1
    #Check the receipt number is not blank and between 5 and 10, set error text if blankif (entry_campers.get().isdigit()) : 
        if  int(entry_receipt.get()) < 5 or  int(entry_receipt.get()) > 10:
            Label(main_window,fg="red", text="5-10 only") .grid(column=2,row=2)
            input_check = 1
    else :
        Label(main_window,fg="red", text="5-10 only") .grid(column=2,row=2)
        input_check = 1
    #Check that amount is not blank, set error text if blank     
    if len(entry_amount.get()) == 0 :
        Label(main_window,fg="red", text="Required") .grid(column=2,row=3)
        input_check = 1
    if input_check == 0 : enter_name()

#add the next details to the list
def enter_name ():
    #enter each item to its own area of the list
    party_store_details.enter([entry_first_name.get(),entry_last_name.get(),entry_recipt_number.get(),entry_amount.get()])
    #clear the boxes
    entry_first_name.delete(0,'end')
    entry_last_name.delete(0,'end')
    entry_recipt_number.delete(0,'end')
    entry_amount.delete(0,'end')
    counters['total_entries'] += 1

#delete a row from the list
def delete_row ():
    #find which row is to be deleted and delete it
    del party_store_details[int(delete_item.get())]
    counters['total_entries'] -= 1
    name_count = counters['name_count']
    delete_item.delete(0,'end')
    #clear the last item displayed on the GUI
    Label(main_window, text="       ").grid(column=0,row=name_count+7) 
    Label(main_window, text="       ").grid(column=1,row=name_count+7)
    Label(main_window, text="       ").grid(column=2,row=name_count+7)
    Label(main_window, text="       ").grid(column=3,row=name_count+7)
    Label(main_window, text="       ").grid(column=4,row=name_count+7)
    #print all the items in the list
    print_party_store_details()

#create the buttons and labels
def setup_buttons():
    #create all the empty and default labels, buttons and entry boxes. Put them in the correct grid location
    Label(main_window, text="first name") .grid(column=0,row=0,sticky=E)
    Label(main_window, text="last name") .grid(column=0,row=1,sticky=E)
    Button(main_window, text="quit",command=quit,width = 10) .grid(column=4, row=0,sticky=E)
    Button(main_window, text="enter",command=check_inputs) .grid(column=3,row=2)
    Button(main_window, text="Print Details",command=party_store_details,width = 10) .grid(column=4,row=1,sticky=E)
    Label(main_window, text="recipt number") .grid(column=0,row=2,sticky=E)
    Label(main_window, text="amount") .grid(column=0,row=3,sticky=E)
    Label(main_window, text="Row #") .grid(column=3,row=2,sticky=E)
    Button(main_window, text="Delete Row",command=delete_row,width = 10) .grid(column=4,row=3,sticky=E)
    Label(main_window, text="               ") .grid(column=2,row=0)
  

#start the program running
def main():
    #Start the GUI it up
    setup_buttons()
    main_window.mainloop()
    
#create empty list for party store details and empty variable for entries in the list
counters = {'total_entries':0,'name_count':0}
party_store_details = []    
main_window =Tk()
main_window.title("Julie's Party store")
entry_first_name = Entry(main_window)
entry_first_name.grid(column=1,row=0)
entry_last_name = Entry(main_window)
entry_last_name.grid(column=1,row=1)
entry_first_name = Entry(main_window)
entry_first_name.grid(column=1,row=2)
entry_recipt_number = Entry(main_window)
entry_recipt_number.grid(column=1,row=3)
delete_item = Entry(main_window)
delete_item .grid(column=3,row=3)

main()
