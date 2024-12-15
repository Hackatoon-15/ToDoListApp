import itertools
import json

fold = "fold.json"

def by_priority(task):
    return task['Priority']

def by_dueDate(task):
    return task['Due date']

def view(V):
     while True:
          view = input(V)
          if view.isdigit():                                                  
               return int(view)
          else:
               print("You fool choose a digit")

def View(task, due_date, priority):
    with open(fold, "r+") as org:
        try: 
            task = json.load(org)
        except json.decoder.JSONDecoderError:
            task = []

        print("1.By Priority\n2.Due Date\n")
        Watch = view("Choose a view: ")
        output = ()
        if (Watch ==1):
            sort_by_priority = itertools.groupby(sorted(task, key=by_priority), by_priority)
            priority = {key: len(list(val)) for key, val in sort_by_priority}
            output = {'Priority': priority}
        elif (View==2):    
            sort_by_dueDate = itertools.groupby(sorted(task, key=by_dueDate), by_dueDate)
            due_date = {key: len(list(val)) for key, val in sort_by_dueDate} 
            output = {'Due date': due_date} 
        
        org.seek(0) 
        json.dump(output, org, sort_keys=True, indent=4) 
        org.truncate()
