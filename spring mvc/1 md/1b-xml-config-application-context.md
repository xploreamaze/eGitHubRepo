#INSTALL
Spring Tools 3 Add-On from Eclipse Marketplace

#CREATE THE SPRING BEAN CONFIGURATION FILE
#create new source folder
src/main/resources

#create new spring bean configuration file inside resources
[spring-config.xml]
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	<bean id="product" class="com.ezbuy.model.Product">
		<constructor-arg name="productID" value="100" />
		<constructor-arg name="productName" value="Red" />
		<constructor-arg name="description" value="Sun" />
	</bean>
	<bean id="product1" class="com.ezbuy.model.Product">
		<property name="productID" value="200"></property>
		<property name="productName" value="Angular"></property>
		<property name="description" value="Front End JS Framework"></property>
	</bean>
</beans>

#CREATE APP TO USE THE BEANS
package com.ezbuy;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

import com.ezbuy.model.Product;

public class App {
	public static void main(String[] args) {
		System.out.println("Welcome to eZBuy");
		AbstractApplicationContext applicationContext = new ClassPathXmlApplicationContext(
				"spring-config.xml");
//		AbstractApplicationContext applicationContext = new FileSystemXmlApplicationContext(
//				"C:\\users\\subbu\\desktop\\spring-config.xml");
		
		System.out.println("\nproduct");
		Product product = (Product) applicationContext.getBean("product");
		System.out.println(product);
		product.setProductName("GreenMoon");
		System.out.println(product);
		System.out.println("\nproduct1");

		System.out.println(applicationContext.getBean("product1"));
	}
}

#CREATE THE MODEL
package com.ezbuy.model;
//Creating the product bean
public class Product {

	int productID;
	String productName;
	String description;
	public Product() {
		System.out.println("Product()");
	}

	public Product(int productID, String productName, String description) {
		super();
		System.out.println("Product(int productID, String productName, String description)");
		this.productID = productID;
		this.productName = productName;
		this.description = description;
	}

	public String getDescription() {
		return description;
	}

	public int getProductID() {
		return productID;
	}

	public String getProductName() {
		return productName;
	}

	public void setDescription(String description) {
		this.description = description;
	}

	public void setProductID(int productID) {
		System.out.println("setProductID(int productID)");
		this.productID = productID;
	}

	public void setProductName(String productName) {
		this.productName = productName;
	}

	@Override
	public String toString() {
		return "Product [productID=" + productID + ", productName=" + productName + ", description=" + description
				+ "]";
	}

}



