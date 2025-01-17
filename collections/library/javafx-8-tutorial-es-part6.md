---
layout: article
title: "JavaFX 8 Tutorial - Part 6: Statistics Chart"
date: 2014-09-17 00:00
updated: 2014-09-17 00:00
slug: javafx-8-tutorial/es/part6
canonical: /java/javafx-8-tutorial-part6/
github: https://github.com/marcojakob/code.makery.ch/edit/master/collections/library/javafx-8-tutorial-es-part6.md
description: "Learn how to create a JavaFX Bar Chart."
image: /assets/library/javafx-8-tutorial/part6/addressapp-part6.png
published: true
prettify: true
comments: true
sidebars:
- header: "Artículos en esta serie"
  body:
  - text: "Introducción"
    link: /library/javafx-8-tutorial/es/
    paging: Intro
  - text: "Parte 1: Scene Builder"
    link: /library/javafx-8-tutorial/es/part1/
    paging: 1
  - text: "Parte 2: Modelo y TableView"
    link: /library/javafx-8-tutorial/es/part2/
    paging: 2
  - text: "Parte 3: Interacción con el usuario"
    link: /library/javafx-8-tutorial/es/part3/
    paging: 3
  - text: "Parte 4: Hojas de estilo CSS"
    link: /library/javafx-8-tutorial/es/part4/
    paging: 4
  - text: "Parte 5: Persistencia de datos con XML"
    link: /library/javafx-8-tutorial/es/part5/
    paging: 5
  - text: "Parte 6: Gráficos estadísticos"
    link: /library/javafx-8-tutorial/es/part6/
    paging: 6
    active: true
  - text: "Parte 7: Publicación con e(fx)clipse"
    link: /library/javafx-8-tutorial/es/part7/
    paging: 7
- header: Lenguajes
  body:
  - text: English
    link: /java/javafx-8-tutorial-part6/
    icon-css: fa fa-fw fa-globe
  - text: Português
    link: /library/javafx-8-tutorial/pt/part6/
    icon-css: fa fa-fw fa-globe
  - text: Español
    link: /library/javafx-8-tutorial/es/part6/
    icon-css: fa fa-fw fa-globe
    active: true
---

<div class="alert alert-warning">
  <i class="fa fa-language"></i> This page is beeing translated to Spanish. If you'd like to help out please read <a href="/library/how-to-contribute/" class="alert-link">how to contribute</a>.
</div>

![Screenshot AddressApp Part 6](/assets/library/javafx-8-tutorial/part6/addressapp-part6.png)


## Topics in Part 6

* Creating a **Statistics Chart** to display birthday distribution.


*****

## Birthday Statistics

All our people in the AddressApp have a birthday. Wouldn't it be nice to have some statistics about when our people celebrate their birthday.

We'll use a **Bar Chart** containing a bar for each month. Each bar shows how many people have their birthday in that particular month.


## The Statistics FXML View

1. We start by creating a `BirthdayStatistics.fxml` file inside our `ch.makery.address.view` package (*Right-click on package | New | other... | New FXML Document*).   
![Birthday Statistics FXML](/assets/library/javafx-8-tutorial/part6/birthday-statistics-fxml.png)

2. Open the `BirthdayStatistics.fxml` file in Scene Builder.

3. Select the root `AnchorPane`. In the *Layout* group set the *Pref Width* to 620 and the *Pref Height* to 450.

4. Add a `BarChart` to the `AnchorPane`.

5. Right-click on the `BarChart` and select *Fit to Parent*.

6. Save the fxml file, go to Eclipse and refresh the project.

Before we'll come back to Scene Builder we'll first create the controller and wire everything up in our `MainApp`.


## The Statistics Controller

In the view package `ch.makery.address.view` create a Java class called `BirthdayStatisticsController.java`.

Let's first take a look at the entire controller class before I start explaining:


##### BirthdayStatisticsController.java

<pre class="prettyprint lang-java">
package ch.makery.address.view;

import java.text.DateFormatSymbols;
import java.util.Arrays;
import java.util.List;
import java.util.Locale;

import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.fxml.FXML;
import javafx.scene.chart.BarChart;
import javafx.scene.chart.CategoryAxis;
import javafx.scene.chart.XYChart;
import ch.makery.address.model.Person;

/**
 * The controller for the birthday statistics view.
 * 
 * @author Marco Jakob
 */
public class BirthdayStatisticsController {

    @FXML
    private BarChart&lt;String, Integer> barChart;

    @FXML
    private CategoryAxis xAxis;

    private ObservableList&lt;String> monthNames = FXCollections.observableArrayList();

    /**
     * Initializes the controller class. This method is automatically called
     * after the fxml file has been loaded.
     */
    @FXML
    private void initialize() {
        // Get an array with the English month names.
        String[] months = DateFormatSymbols.getInstance(Locale.ENGLISH).getMonths();
        // Convert it to a list and add it to our ObservableList of months.
        monthNames.addAll(Arrays.asList(months));
        
        // Assign the month names as categories for the horizontal axis.
        xAxis.setCategories(monthNames);
    }

    /**
     * Sets the persons to show the statistics for.
     * 
     * @param persons
     */
    public void setPersonData(List&lt;Person> persons) {
    	// Count the number of people having their birthday in a specific month.
        int[] monthCounter = new int[12];
        for (Person p : persons) {
            int month = p.getBirthday().getMonthValue() - 1;
            monthCounter[month]++;
        }

        XYChart.Series&lt;String, Integer> series = new XYChart.Series&lt;>();
        
        // Create a XYChart.Data object for each month. Add it to the series.
        for (int i = 0; i &lt; monthCounter.length; i++) {
        	series.getData().add(new XYChart.Data&lt;>(monthNames.get(i), monthCounter[i]));
        }
        
        barChart.getData().add(series);
    }
}
</pre>


#### How the Controller Works

1. The controller will need access to two elements from our FXML file:
   * The `barChar`: It has the type `String` and `Integer`. The `String` is used for the month on the x-axis and the `Integer` is used for the number of people in a specific month. 
   * The `xAxis`: We'll use this to add the month Strings.   

2. The `initialize()` method fills the x-axis with a list of all the months.

3. The `setPersonData(...)` method will be accessed by the `MainApp` class to set the person data. It loops through all persons and counts the birthdays per month. Then it adds `XYChart.Data` for every month to the data series. Each `XYChart.Data` object will represent one bar in the chart.


*****

## Connecting View and Controller

1. Open `BirthdayStatistics.fxml` in Scene Builder.

2. In the *Controller* group set `BirthdayStatisticsController` as controller.

3. Select the `BarChart` and choose `barChart` as fx:id Property (in the *Code* group).

4. Select the `CategoryAxis` and choose `xAxis` as fx:id Property.   
![Category Axis](/assets/library/javafx-8-tutorial/part6/category-axis.png)

5. You may add a title to the `BarChart` (in *Properties* group) for further styling.



*****


## Connecting the View/Controller with MainApp

We'll use the same mechanism for our *birthday statistics* that we used for the *edit person dialog*, a simple popup dialog.

Add the following method to your `MainApp` class:


<pre class="prettyprint lang-java">
/**
 * Opens a dialog to show birthday statistics.
 */
public void showBirthdayStatistics() {
    try {
        // Load the fxml file and create a new stage for the popup.
        FXMLLoader loader = new FXMLLoader();
        loader.setLocation(MainApp.class.getResource("view/BirthdayStatistics.fxml"));
        AnchorPane page = (AnchorPane) loader.load();
        Stage dialogStage = new Stage();
        dialogStage.setTitle("Birthday Statistics");
        dialogStage.initModality(Modality.WINDOW_MODAL);
        dialogStage.initOwner(primaryStage);
        Scene scene = new Scene(page);
        dialogStage.setScene(scene);

        // Set the persons into the controller.
        BirthdayStatisticsController controller = loader.getController();
        controller.setPersonData(personData);

        dialogStage.show();

    } catch (IOException e) {
        e.printStackTrace();
    }
}
</pre>

Everything is set up, but we don't have anything that actually calls the new `showBirthdayStatistics()` method. Luckily we already have a menu in `RootLayout.fxml` that can be used for this purpose.


### Show Birthday Statistics Menu

In your `RootLayoutController` add the following method which will handle user clicks on the *show birthday statistics* menu item: 

<pre class="prettyprint lang-java">
/**
 * Opens the birthday statistics.
 */
@FXML
private void handleShowBirthdayStatistics() {
  mainApp.showBirthdayStatistics();
}
</pre>

Now, open the `RootLayout.fxml` file with Scene Builder. Create the *Statistics* `Menu` with a *Show Statistics* `MenuItem`:

![Show Statistics Menu](/assets/library/javafx-8-tutorial/part6/show-statistics-menu.png)

Select the *Show Statistics* `MenuItem` and choose `handleShowBirthdayStatistics` for `On Action` (in *Code* group)   

![Show Statistics On Action](/assets/library/javafx-8-tutorial/part6/show-statistics-on-action.png)

Go to Eclipse, refresh the project and **test it**.


*****

## More Information on JavaFX Charts

A good place for more information is the official Oracle tutorial on [Working with JavaFX Charts](http://docs.oracle.com/javase/8/javafx/user-interface-tutorial/charts.htm).


### What's Next?

In the last tutorial [Part 7](/java/javafx-8-tutorial-part7/) we will finally deploy our application (i.e. package and deliver the app to our users).


##### Some other articles you might find interesting

* [JavaFX Dialogs](/blog/javafx-8-dialogs/)
* [JavaFX Date Picker](/blog/javafx-8-date-picker/)
* [JavaFX Event Handling Examples](/blog/javafx-8-event-handling-examples/)
* [JavaFX TableView Sorting and Filtering](/blog/javafx-8-tableview-sorting-filtering/)
* [JavaFX TableView Cell Renderer](/blog/javafx-8-tableview-cell-renderer/)

