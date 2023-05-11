# assignment09May
fileName = "c:\\Huzaifa\\assignment\\countryData.csv"
totalPopD=0       #
counter = 0       #Initiliasation
countryArray = [] #

myFile = open(fileName, "r+")

readData = myFile.readline() #First line is headings only so we don't need any processing on that data

readData = myFile.readline()
while len(readData) > 0:    #Loop stops when empty line is read
    countryTuple = readData.split(',') #Creates a list containing a single record
    countryTuple[3] = countryTuple[3].strip("\n") #Because new line is to be moved after PopDensity entry
    populationDensity = float(countryTuple[3])/float(countryTuple[2])
    countryTuple.append(populationDensity)
    totalPopD += populationDensity       
    counter += 1                         #To calculate average after loop
    countryArray.append(countryTuple)    #Appends to a list which will contain all complete records

    readData = myFile.readline()

avgPopD = totalPopD/counter

myFile.close()

newFile = open("belowAverage.csv","w") #Creating new file to store data of countries with below average popDensity
newFile.write("Code" + "," + "Name" + "," + "SurfaceArea" + "," + "Population" + "," + "PopulationDensity"+"\n")

for i in range(len(countryArray)):
    if (countryArray[i][4] < avgPopD): #Condition to check if popDensity is below average
        newFile.write(countryArray[i][0] + "," + countryArray[i][1] + "," + countryArray[i][2] + "," + countryArray[i][3] + "," + str(round(countryArray[i][4],1)) + "\n")


newFile.close()
