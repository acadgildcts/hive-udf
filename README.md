# hive-udf
program----------------
import java.util.ArrayList;

import org.apache.hadoop.hive.ql.exec.UDF; 
import org.apache.hadoop.io.Text;

public class udf extends UDF{ 
	public Text evaluate(String str ,ArrayList<String> str1) 
	{ 
		StringBuffer sb = new StringBuffer(); 
		for (int i = 0; i < str1.size(); i++) 
		{ 
			sb.append(str1.get(i)); 
			sb.append(str);

	}
	return new Text(sb.toString());
	
}

}





commands-------------------
hive> add jar /home/acadgild/Desktop/udfnew.jar;
Added [/home/acadgild/Desktop/udfnew.jar] to class path
Added resources: [/home/acadgild/Desktop/udfnew.jar]
hive> create temporary function concat as 'udf';
OK
Time taken: 1.004 seconds
hive> create table udfnew(sep String,arr array<String>)
    > row format delimited 
    > fields terminated by ','
    > collection items terminated by '#';
OK
Time taken: 1.096 seconds
hive> load data local inpath '/home/acadgild/Desktop/hive' into table udfnew;
Loading data to table default.udfnew
OK
Time taken: 1.111 seconds
hive> select * from udfnew
    > ;
OK
--	["data","acad"]
++	["big","acad"]
Time taken: 1.921 seconds, Fetched: 2 row(s)
hive> select concat(*) from udfnew
    > ;
OK
data--acad--
big++acad++
Time taken: 0.491 seconds, Fetched: 2 row(s)
hive> 

