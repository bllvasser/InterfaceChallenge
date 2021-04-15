InterfaceChallenge
package com.company;

import java.util.List;
import java.util.ArrayList;

public interface ISaveable {
    List<String> write();
    void read(List<String> savedValues);
}
package com.company;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class Player implements ISaveable {
    private String name;
    private String weapon;
    private int hitPoints;
    private int strength;

    public Player(int hitPoints, int strength, String name) {
        this.hitPoints = hitPoints;
        this.name = name;
        this.strength = strength;
        this.weapon = weapon;
    }

    @Override
    public List<String> write() {
        List<String> values = new ArrayList<String>();
        values.add(0, this.name);
        values.add(1, "" + this.hitPoints);
        values.add(2, "" + this.strength);
        values.add(3, this.weapon);

        return values;
    }


    @Override
    public void read(List<String> savedValues) {

        if (savedValues != null && savedValues.size() > 0) {
            this.name = savedValues.get(0);
            this.hitPoints = Integer.parseInt(savedValues.get(1));
            this.strength = Integer.parseInt(savedValues.get(2));
            this.weapon = savedValues.get(3);
        }
    }

    @Override
    public String toString() {
        return "Player{" +
                "name='" + name + '\'' +
                ", weapon='" + weapon + '\'' +
                ", hitPoints=" + hitPoints +
                ", strength=" + strength +
                '}';
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getWeapon() {
        return weapon;
    }

    public void setWeapon(String weapon) {
        this.weapon = weapon;
    }

    public int getHitPoints() {
        return hitPoints;
    }

    public void setHitPoints(int hitPoints) {
        this.hitPoints = hitPoints;
    }

    public int getStrength() {
        return strength;
    }

    public void setStrength(int strength) {
        this.strength = strength;
    }
}
package com.company;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class Monster implements ISaveable {
    private String name;
    private int hitPoints;
    private int strength;

    public Monster(String name, int hitPoints, int strength) {
        this.hitPoints = hitPoints;
        this.name = name;
        this.strength = strength;
    }


    public List<String> write() {
        List<String> values = new ArrayList<String>();
        values.add(0, this.name);
        values.add(1, "" + this.hitPoints);
        values.add(2, "" + this.strength);

        return values;
    }


    public void read(List<String> savedValues) {

        if (savedValues != null && savedValues.size() > 0) {
            this.name = savedValues.get(0);
            this.hitPoints = Integer.parseInt(savedValues.get(1));
            this.strength = Integer.parseInt(savedValues.get(2));
        }
    }

    @Override
    public String toString() {
        return "Player{" +
                "name='" + name + '\'' +
                ", hitPoints=" + hitPoints +
                ", strength=" + strength +
                '}';
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getHitPoints() {
        return hitPoints;
    }

    public void setHitPoints(int hitPoints) {
        this.hitPoints = hitPoints;
    }

    public int getStrength() {
        return strength;
    }

    public void setStrength(int strength) {
        this.strength = strength;
    }
}
package com.company;

import java.util.LinkedList;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Main {


    public static void main(String[] args) {

        Player bilaal = new Player(10, 100, "Links");
        System.out.println(bilaal.toString());
        saveObjects(bilaal);
        bilaal.setHitPoints(25);
        System.out.println(bilaal);
        bilaal.setWeapon("Master Sword");
        saveObjects(bilaal);
        loadObjects(bilaal);
        System.out.println(bilaal);

        ISaveable enemy = new Monster("Gannondorf", 50, 500);
        System.out.println(enemy);
        saveObjects(enemy);

    }

    public static List<String> readValues() {
        List<String> values = new ArrayList<String>();

        Scanner scanner = new Scanner(System.in);
        boolean quit = false;
        int index = 0;
        System.out.println("Choose\n" +
                "1 to enter a String\n" +
                "0 to quit");

        while (!quit) {
            System.out.println("Choose an option:");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 0:
                    quit = true;
                    break;

                case 1:
                    System.out.println("Enter a string: ");
                    String stringInput = scanner.nextLine();
                    values.add(index, stringInput);
                    index++;
                    break;
            }
        }
        return values;
    }

    public static void saveObjects(ISaveable objectsToSave) {
        for (int i = 0; i < objectsToSave.write().size(); i++) {
            System.out.println("saving" + objectsToSave.write().get(i) + "to storage");
        }
    }

    public static void loadObjects(ISaveable objectsToLoad) {
        List<String> values = readValues();
        objectsToLoad.read(values);
    }
}
/Library/Java/JavaVirtualMachines/amazon-corretto-11.jdk/Contents/Home/bin/java "-javaagent:/Applications/IntelliJ IDEA CE.app/Contents/lib/idea_rt.jar=54503:/Applications/IntelliJ IDEA CE.app/Contents/bin" -Dfile.encoding=UTF-8 -classpath /Users/Bilaal/IdeaProjects/InterfaceChallenge/out/production/InterfaceChallenge com.company.Main
Player{name='Links', weapon='null', hitPoints=10, strength=100}
savingLinksto storage
saving10to storage
saving100to storage
savingnullto storage
Player{name='Links', weapon='null', hitPoints=25, strength=100}
savingLinksto storage
saving25to storage
saving100to storage
savingMaster Swordto storage
Choose
1 to enter a String
0 to quit
Choose an option:
0
Player{name='Links', weapon='Master Sword', hitPoints=25, strength=100}
Player{name='Gannondorf', hitPoints=50, strength=500}
savingGannondorfto storage
saving50to storage
saving500to storage

Process finished with exit code 0
