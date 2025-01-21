#---------------------------------------------------
#------Created  : 18/01/2025 - Mohammad Sami
#------Modified : 
#------Description : BP_status_assignment_draft
#----------------------------------------------------


#-----Define Funtions---------------
def calculate_average(scores):
    return sum(scores) / len(scores)

def assign_Status(average):
    if average <= 120:
        return 'Low'
    elif average >= 140:
        return 'High'
    else:
        return 'Normal'
    
#-----End Functions---------------

#-------Define GpReferral-----------
def GpReferral(Status):
     if Status == Normal:
          return 'Do not refer to GP'
     elif Status == Low:
          return 'Come back for checkup'
     else: 
          return 'Book an appointment with GP'
     
#-----------End Functions---------------------

# importing csv module
import csv



# initializing the patients list
BP = []

# reading csv file
with open('BP_sysdias.csv', 'r') as file:
        # creating a csv reader object
        reader = csv.reader(file)

        # Read the header (first row)
        header = next(reader) 
        
        # extracting field names through first row
        for row in reader:
            Reading, Reading1, Reading2, Reading3 = row
            average = calculate_average([int(Reading1), int(Reading2), int(Reading3)])
            Status = assign_Status(average)
            GpReferral = assign_GpReferral
            BP.append([Reading, Reading1, Reading2, Reading3, average, Status, GpReferral])

with open('BP_sysdias_output.csv', 'w', newline='') as file:
        writer = csv.writer(file) 
        writer.writerow(['Reading', 'Reading1', 'Reading2', 'Reading3', 'Average', 'Status'])
        writer.writerows(BP)

print('Results saved to BP_sysdias_output.csv')




