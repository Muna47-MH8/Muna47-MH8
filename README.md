question 2


import java.util.*;

// Base class for participants
class Participant {
    private String name;
    private int id;
    private int swimmingTime;
    private int cyclingTime;
    private int runningTime;

    // Constructor
    public Participant(String name, int id, int swimmingTime, int cyclingTime, int runningTime) {
        if (swimmingTime < 0 || cyclingTime < 0 || runningTime < 0) {
            throw new IllegalArgumentException("Times cannot be negative.");
        }
        this.name = name;
        this.id = id;
        this.swimmingTime = swimmingTime;
        this.cyclingTime = cyclingTime;
        this.runningTime = runningTime;
    }

    // Getters and setters
    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }

    public int getSwimmingTime() {
        return swimmingTime;
    }

    public void setSwimmingTime(int swimmingTime) {
        if (swimmingTime < 0) {
            throw new IllegalArgumentException("Swimming time cannot be negative.");
        }
        this.swimmingTime = swimmingTime;
    }

    public int getCyclingTime() {
        return cyclingTime;
    }

    public void setCyclingTime(int cyclingTime) {
        if (cyclingTime < 0) {
            throw new IllegalArgumentException("Cycling time cannot be negative.");
        }
        this.cyclingTime = cyclingTime;
    }

    public int getRunningTime() {
        return runningTime;
    }

    public void setRunningTime(int runningTime) {
        if (runningTime < 0) {
            throw new IllegalArgumentException("Running time cannot be negative.");
        }
        this.runningTime = runningTime;
    }

    // Method to calculate total time
    public int calculateTotalTime() {
        return swimmingTime + cyclingTime + runningTime;
    }

    // Display details
    public void displayDetails() {
        System.out.printf("Name: %s, ID: %d, Total Time: %d minutes\n", name, id, calculateTotalTime());
    }
}

// Derived class for elite participants
class EliteParticipant extends Participant {
    private String sponsorName;

    // Constructor
    public EliteParticipant(String name, int id, int swimmingTime, int cyclingTime, int runningTime, String sponsorName) {
        super(name, id, swimmingTime, cyclingTime, runningTime);
        this.sponsorName = sponsorName;
    }

    public String getSponsorName() {
        return sponsorName;
    }

    public void setSponsorName(String sponsorName) {
        this.sponsorName = sponsorName;
    }

    @Override
    public void displayDetails() {
        super.displayDetails();
        System.out.printf("Sponsor: %s\n", sponsorName);
    }
}

// Derived class for beginner participants
class BeginnerParticipant extends Participant {
    public BeginnerParticipant(String name, int id, int swimmingTime, int cyclingTime, int runningTime) {
        super(name, id, swimmingTime, cyclingTime, runningTime);
    }
}

// Main class
public class TriathlonResults {
    public static void main(String[] args) {
        // Create participants
        List<Participant> participants = new ArrayList<>();
        participants.add(new Participant("Alice", 1, 25, 40, 20));
        participants.add(new Participant("Bob", 2, 20, 35, 25));
        participants.add(new Participant("Charlie", 3, 30, 50, 30));
        participants.add(new Participant("Diana", 4, 28, 42, 18));

        // Calculate total times and sort participants by total time
        participants.sort(Comparator.comparingInt(Participant::calculateTotalTime));

        // Display sorted results
        System.out.println("Sorted Results:");
        for (Participant p : participants) {
            p.displayDetails();
        }

        // Determine and print the fastest and second fastest participants
        if (participants.size() > 0) {
            System.out.println("\nFastest Participant:");
            participants.get(0).displayDetails();
        }
        if (participants.size() > 1) {
            System.out.println("\nSecond Fastest Participant:");
            participants.get(1).displayDetails();
        }

        // Handle ties in total time
        System.out.println("\nParticipants with Same Total Time:");
        for (int i = 0; i < participants.size() - 1; i++) {
            if (participants.get(i).calculateTotalTime() == participants.get(i + 1).calculateTotalTime()) {
                participants.get(i).displayDetails();
                participants.get(i + 1).displayDetails();
            }
        }
    }
}



