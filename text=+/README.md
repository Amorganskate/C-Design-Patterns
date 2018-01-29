# Data Access


    
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
        

