# validation_Code
//validating a login page and capture error message using webelement and driver methods.


package web_driver;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class Verify_error_message {

	public static void main(String[] args) throws Throwable {
		// TODO Auto-generated method stub
		System.setProperty( "webdriver.chrome.driver","E:\\Chromedriver.exe");
		WebDriver driver = new ChromeDriver();
		driver.manage().window().maximize();
		driver.manage().deleteAllCookies();
		driver.get("http://orangehrm.qedgetech.com/");
		Thread.sleep(5000);
		WebElement username =driver.findElement(By.xpath("//input[@id='txtUsername']"));
		username.clear();
		username.sendKeys("Admin");
		String user =username.getAttribute("value");
		WebElement password =driver.findElement(By.xpath("//input[@id='txtPassword']"));
		password.clear();
        password.sendKeys("Qedge123!@#");
        String pass =password.getAttribute("value");
        
        driver.findElement(By.xpath("//input[@id='btnLogin']")).click();
        System.out.println(user+"  "+pass);
        String Expected ="dashboard";
        String Actual =driver.getCurrentUrl();
        if(Actual.contains(Expected))
        {
        	System.out.println("Login Success::"+Expected+"  "+Actual);
        }
        else{
        	String error_message =driver.findElement(By.xpath("//span[@id='spanMessage']")).getText();
        	System.out.println(error_message +Expected+"  "+Actual);
        }
        driver.close();
	}

}

