# PyBoss
Takes a CSV file with some employee data and reformats it for a different HR system 
# Modules
import os
import csv

us_state_abbrev = {
    'Alabama': 'AL',
    'Alaska': 'AK',
    'Arizona': 'AZ',
    'Arkansas': 'AR',
    'California': 'CA',
    'Colorado': 'CO',
    'Connecticut': 'CT',
    'Delaware': 'DE',
    'Florida': 'FL',
    'Georgia': 'GA',
    'Hawaii': 'HI',
    'Idaho': 'ID',
    'Illinois': 'IL',
    'Indiana': 'IN',
    'Iowa': 'IA',
    'Kansas': 'KS',
    'Kentucky': 'KY',
    'Louisiana': 'LA',
    'Maine': 'ME',
    'Maryland': 'MD',
    'Massachusetts': 'MA',
    'Michigan': 'MI',
    'Minnesota': 'MN',
    'Mississippi': 'MS',
    'Missouri': 'MO',
    'Montana': 'MT',
    'Nebraska': 'NE',
    'Nevada': 'NV',
    'New Hampshire': 'NH',
    'New Jersey': 'NJ',
    'New Mexico': 'NM',
    'New York': 'NY',
    'North Carolina': 'NC',
    'North Dakota': 'ND',
    'Ohio': 'OH',
    'Oklahoma': 'OK',
    'Oregon': 'OR',
    'Pennsylvania': 'PA',
    'Rhode Island': 'RI',
    'South Carolina': 'SC',
    'South Dakota': 'SD',
    'Tennessee': 'TN',
    'Texas': 'TX',
    'Utah': 'UT',
    'Vermont': 'VT',
    'Virginia': 'VA',
    'Washington': 'WA',
    'West Virginia': 'WV',
    'Wisconsin': 'WI',
    'Wyoming': 'WY',
}

# Lists to store data
emp_id = []
name = []
dob = []
ssn = []
state = []
first_name = []
last_name = []

# Set path for file
csvpath = os.path.join(".", "Documents", "PyBoss_employee_data.csv")

# Open the CSV
with open(csvpath, newline="", encoding='utf-8') as csvfile:
    csvreader = csv.reader(csvfile)
    
    
    
    # how do I skip first row of reads????
    # and what is wrong with my re-sub?
    # and I can't find the second data file 
    #
    # Loop through the CSV file grabbing the data and placing into variables 
    for row in csvreader:
         emp_id.append(row[0])  #start easy, add employee id to emp_id list 
         
         temp_name=row[1]       #take out the first name and put into temp_name variable 
         first, last = temp_name.split(' ') #split into first and last name 
         first_name.append(first) #append both to their respective list
         last_name.append(last)
          
         temp_dob=row[2]  #put DOB into temp_DOB for some manipulating
         year, month, day = temp_dob.split('-')  #split DOB into 3 variables separated by -
         new_date_format= month + '/' + day + '/' + year
         dob.append(new_date_format)
       
         temp_ssn = row[3]
         #temp_ssn = re.sub('\d{3}', 'xxx', temp_ssn,1)
         #temp_ssn = re.sub('\d{2}', 'xx', temp_ssn,1)   
         ssn.append(temp_ssn)
     
         temp_state=row[4]   
         temp_state=us_state_abbrev[temp_state]
         state.append(temp_state)

        #end of reading and manipulating employee data, time to write!       
        
        
         # Zip lists together
         cleaned_csv = zip(emp_id, first_name, last_name,dob, ssn, state)

         # Set variable for output file
         output_file = os.path.join("employee_data_cleaned.csv")
  
         with open(output_file, "w", newline="") as datafile:
            writer = csv.writer(datafile)

            # Write the header row
            writer.writerow(["Emp ID", "First Name", "Last Name", "DOB", "SSN", "State"])

            # Write in zipped rows
            writer.writerows(cleaned_csv)


            #emp_id.append(row[0])
            #print(emp_id)
  

    

