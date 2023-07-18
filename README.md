# Apitesting-maven-run-May2023
Test case1
package com.restTests.simpleTests;

import java.util.ArrayList;

import org.hamcrest.Matcher;
import org.hamcrest.Matchers;
import org.testng.Assert;
import org.testng.annotations.Test;

import io.restassured.RestAssured;
import io.restassured.http.ContentType;
import io.restassured.response.Response;
import io.restassured.specification.RequestSpecification;

// Base url = https://dummy.restapiexample.com/api/v1/employees

public class SimpleRestRequest {
	@Test
	public void restapi() {
		
		RequestSpecification req= RestAssured.given();
		 Response res=req.when()
				 		 .get("https://dummy.restapiexample.com/api/v1/employees\r\n"
				 		 		+ "");
		 res.then().contentType(ContentType.JSON);
		 res.then().statusCode(200);
		 res.then().time(Matchers.lessThan(4000L));
		 
		 res.prettyPrint();
	}	
}
		
Test case 2
package com.restTests.simpleTests;

import org.testng.Assert;

import org.testng.annotations.Test;
import io.restassured.RestAssured;
import io.restassured.response.Response;

public class CreateRequest {
  

 
  @Test
  public void testCreateEndpoint() {
    // Perform API request using REST-assured
    Response response = RestAssured
        .given()
        .contentType("application/json")
        .body("{\"name\":\"test\",\"salary\":\"123\",\"age\":\"23\"}")
        .when()
        .post(" https://dummy.restapiexample.com/api/v1/employees");
        		
    // Extract response data
    String status = response.jsonPath().getString("status");
    String name = response.jsonPath().getString("data.name");
    String salary = response.jsonPath().getString("data.salary");
    String age = response.jsonPath().getString("data.age");
    int id = response.jsonPath().getInt("data.id");

    // Assert expected values
    Assert.assertEquals(status, "success");
    Assert.assertEquals(name, "test");
    Assert.assertEquals(salary, "123");
    Assert.assertEquals(age, "23");
    Assert.assertTrue(id > 0);
  }
}
Test case :3
package com.restTests.simpleTests;

import org.testng.Assert;


import org.testng.annotations.Test;
import io.restassured.RestAssured;
import io.restassured.response.Response;

public class DeleteRequest1 {

	 @Test
	  public void testDeleteEndpoint() {
	    // Perform API request using REST-assured
	    Response response = RestAssured
	        .given()
	        .contentType("application/json")
	        .body("{\"name\":\"test\",\"salary\":\"123\",\"age\":\"23\"}")
	        .when()
	        .post("http://dummy.restapiexample.com/api/v1/employees");

	    // Extract response data
	    String status = response.jsonPath().getString("status");
	    String name = response.jsonPath().getString("data.name");
	    String salary = response.jsonPath().getString("data.salary");
	    String age = response.jsonPath().getString("data.age");
	    int id = response.jsonPath().getInt("data.id");
	    // Assert expected values
	    Assert.assertEquals(status, "success");
	    Assert.assertEquals(name, "test");
	    Assert.assertEquals(salary, "123");
	    Assert.assertEquals(age, "23");
	    Assert.assertTrue(id > 0);
	  }
	}
Test case 4
package com.restTests.simpleTests;

import io.restassured.RestAssured;
import io.restassured.response.Response;

public class DeleteRequest2 {

	 public static void main(String[] args) {
	        // Assuming you have the necessary dependencies, such as REST-assured, set up correctly

	        // Construct the URL for the delete request
	        String deleteUrl = "http:// dummy.restapiexample.com/api/v1/employees/delete/0";

	        // Send DELETE request using REST-assured
	        Response response = RestAssured.delete(deleteUrl);

	        // Validate the response
	        int statusCode = response.getStatusCode();
	        String responseBodyStatus = response.jsonPath().getString("status");
	        String message = response.jsonPath().getString("message");
	        // Assert the status code
	        if (statusCode == 400) {
	            System.out.println("Status code is 400 (Bad Request) - Passed");
	        } else {
	            System.out.println("Status code is not 400 - Failed");
	        }

	        // Assert the response body status
	        if (responseBodyStatus.equals("error")) {
	            System.out.println("Response body status is 'error' - Passed");
	        } else {
	            System.out.println("Response body status is not 'error' - Failed");
	        }

	        // Print the message data
	        System.out.println("Message: " + message);
	    }
	}

Test case 5
package com.restTests.simpleTests;

import io.restassured.RestAssured;
import io.restassured.http.ContentType;
import io.restassured.response.Response;

public class Request5 {

	 public static void main(String[] args) {
	        // Assuming you have the necessary dependencies, such as REST-assured, set up correctly

	        // Construct the URL for the GET request
	        String getUrl = "http://dummy.restapiexample.com/api/v1/employee/2";

	        // Send GET request using REST-assured
	        Response response = RestAssured.get(getUrl);
	        // Validate the response
	        int statusCode = response.getStatusCode();
	        String contentType = response.contentType();
	        String employeeName = response.jsonPath().getString("name");
	        String employeeSalary = response.jsonPath().getString("salary");
	        String employeeAge = response.jsonPath().getString("age");

	        // Assert the status code
	        if (statusCode == 200) {
	            System.out.println("Status code is 200 - Passed");
	        } else {
	            System.out.println("Status code is not 200 - Failed");
	        }

	        // Assert the content type
	        if (contentType == ContentType.JSON) {
	            System.out.println("Content type is JSON - Passed");
	        } else {
	            System.out.println("Content type is not JSON - Failed");
	        }

	        // Assert the employee name
	        if (employeeName.equals("Garrett Winters")) {
	            System.out.println("Employee name is Garrett Winters - Passed");
	        } else {
	            System.out.println("Employee name is not Garrett Winters - Failed");
	        }

	        // Assert the employee salary
	        if (employeeSalary.equals("170750")) {
	            System.out.println("Employee salary is 170750 - Passed");
	        } else {
	            System.out.println("Employee salary is not 170750 - Failed");
	        }

	        // Assert the employee age
	        if (employeeAge.equals("63")) {
	            System.out.println("Employee age is 63 - Passed");
	        } else {
	            System.out.println("Employee age is not 63 - Failed");
	        }
	    }
	}

