## MySQL II

![](img/2020-08-14-09-32-24.png)



- **Step 1, save search results to database**
- Step 1.1, Under db.mysql package, create class MySQLConnection.java.

![](img/2020-08-13-02-25-27.png)

- Step 1.2, implement DBConnection interface:

```java
public class MySQLConnection implements DBConnection {

	@Override
	public void close() {
		// TODO Auto-generated method stub

	}

	@Override
	public void setFavoriteItems(String userId, List<String> itemIds) {
		// TODO Auto-generated method stub

	}

	@Override
	public void unsetFavoriteItems(String userId, List<String> itemIds) {
		// TODO Auto-generated method stub

	}

	@Override
	public Set<String> getFavoriteItemIds(String userId) {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public Set<Item> getFavoriteItems(String userId) {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public Set<String> getCategories(String itemId) {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public List<Item> searchItems(double lat, double lon, String term) {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public void saveItem(Item item) {
		// TODO Auto-generated method stub

	}

	@Override
	public String getFullname(String userId) {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public boolean verifyLogin(String userId, String password) {
		// TODO Auto-generated method stub
		return false;
	}

}
```


- Step 1.3, implement both close method and constructor. 
  **Again, careful with the import suggestions. Always choose java.sql.*.**


```java
public class MySQLConnection implements DBConnection {

	private Connection conn;

	public MySQLConnection() {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver").getConstructor().newInstance();
			conn = DriverManager.getConnection(MySQLDBUtil.URL);
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

	@Override
	public void close() {
		if (conn != null) {
			try {
				conn.close();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	}
```



- Step 1.4: implement `searchItems()` in `MySQLConnection`. Previously we call 
  TicketMasterClient.search from our SearchItem servlet directly. But actually our 
  recommendation code also needs to call the same search function, so we make a designated 
  function here to do the search call.
  The code is simply copied from what we’ve already had in SearchItem.java.


```java
	@Override
	public List<Item> searchItems(double lat, double lon, String term) {
		TicketMasterClient ticketMasterClient = new TicketMasterClient();
		List<Item> items = ticketMasterClient.search(lat, lon, term);
		for(Item item : items) {
			saveItem(item);
		}
		return items;
	}
```

- Step 1.5, after searchItem, let’s try `saveItem` to save data into database. 
  **Again, careful with the import suggestions. Always choose java.sql.*.**


































