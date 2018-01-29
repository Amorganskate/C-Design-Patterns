# Data Access


### CSharp  
  
  
#### Get All
    public List<"Object"> GetAll()
        {
            using (SqlConnection connection = new SqlConnection(connectionStr))
            {
                SqlCommand cmd = new SqlCommand("Sproc", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                List<"Object"> list = new List<"Object">();

                connection.Open();

                using (XmlReader reader = cmd.ExecuteXmlReader())
                {
                    XmlSerializer serializer = new XmlSerializer(typeof(List<"Object">));
                    while (reader.Read())
                    {
                        if (!reader.IsEmptyElement) { list = (List<"Object">)serializer.Deserialize(reader); }
                    }
                    reader.Close();
                }

                connection.Close();

                return list;
            }
        }
        
        
#### Get By ID
        public "Object" GetByID(int "Object")
        {
            using (SqlConnection connection = new SqlConnection(connectionStr))
            {
                SqlCommand cmd = new SqlCommand("Sproc", connection);
                cmd.CommandType = CommandType.StoredProcedure;
                cmd.Parameters.AddWithValue("SQLParam", Param);

                LiveChatSchedule schedule = null;

                connection.Open();

                using (XmlReader reader = cmd.ExecuteXmlReader())
                {
                    XmlSerializer serializer = new XmlSerializer(typeof("Object"));
                    while (reader.Read())
                    {
                        if (!reader.IsEmptyElement) { schedule = ("Object")serializer.Deserialize(reader); }
                    }
                    reader.Close();
                }

                connection.Close();

                return schedule;
            }
        }
        
#### Update

public bool UpdateDay(int "Param")
{
    using (SqlConnection connection = new SqlConnection(connectionStr))
    {
        SqlCommand cmd = new SqlCommand("Sproc", connection);
        cmd.CommandType = CommandType.StoredProcedure;

        cmd.Parameters.AddWithValue("Param", Param);

        connection.Open();
        bool result = (cmd.ExecuteNonQuery() == 1);
        connection.Close();

        return result;
    }
}

