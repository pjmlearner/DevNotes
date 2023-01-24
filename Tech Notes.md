# Tech Notes

## Software

### Development

#### Data Structures

##### Hash Tables

* what

  * is a dictionary (associated array) that stores a collection of key-value pairs.

* when

  * collect data into a dictionary to use that dictionary to retrieve values based on the key

* how

  ```C#
          Hashtable reportNameHash = new Hashtable();  //create Hash Table
  
  		//get data from oracle DB
          OracleCommand oCmd = new OracleCommand("SELECT CRP_AUTO_KEY, REPLACE(REPLACE(REPORT_NAME,'{?'),'}') REPORT_NAME FROM			CR_PARAMETERS WHERE CRI_AUTO_KEY = " + cri, oConn)
          {
              CommandType = CommandType.Text
          };
  		
  		//add key-value pair to hash table from oracle DB
  		//in this case => key: REPORT_NAME, value: CRP_AUTO_KEY
          OracleDataReader oRdr = oCmd.ExecuteReader();
          while (oRdr.Read())
          {
              reportNameHash.Add(oRdr["REPORT_NAME"], oRdr["CRP_AUTO_KEY"]);
          }
          oCmd.Dispose();
  
          string pSQL = "SELECT PARAM_VALUE, DATE_VALUE FROM CR_PARAMETER_VALUES WHERE STL_AUTO_KEY = " + stl + " AND 					CRP_AUTO_KEY = ";
          oCmd = new OracleCommand("", oConn)
          {
              CommandType = CommandType.Text
          };
  
          foreach (ParameterFieldDefinition paramField in cryrpt.DataDefinition.ParameterFields)
          {
              if (paramField.IsLinked())
              {
                  continue;
              }
              if (paramField.Name == "DATE_TO")
              {
                  cryrpt.SetParameterValue(paramField.Name, "1/1/1960 12:00:00 AM");
              }
              else
              {
                  try
                  {
                      oCmd.CommandText = pSQL + reportNameHash[paramField.Name];  //append the value of the hash record using 																				  the key of the hash
  ```

### DevOps

## Networking

## Misc