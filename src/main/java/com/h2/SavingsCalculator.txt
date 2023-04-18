package com.h2;

import java.time.LocalDate;
import java.time.YearMonth;

public class SavingsCalculator {
    private float [] debits;
    private float [] credits;


    public static void main(String[] args){

        String [] creditsAsString= args[0].split(",");
        String [] debitsAsString= args[1].split(",");

        float [] credits= new float[creditsAsString.length];
        float [] debits= new float[debitsAsString.length];

        for(int i=0; i<creditsAsString.length; i++){
            credits[i]= Float.parseFloat(creditsAsString[i]);
        }

        for(int i=0; i<debitsAsString.length; i++){
            debits[i]= Float.parseFloat(debitsAsString[i]);
        }

        final SavingsCalculator calculator = new SavingsCalculator(credits, debits);
        float netSavings = calculator.calculate();
        System.out.println("Net Savings = " + netSavings + ", remaining days in month = " + remainingDaysInMonth(LocalDate.now()));
    }

    public SavingsCalculator(float []credits, float []debits){
        this.credits=credits;
        this.debits=debits;
    }

    private float sumOfDebits(){
        float sum=0.0f;

        for (float debits: debits){
            sum=sum+debits;
        }
        return sum;
    }

    private float sumOfCredits(){
        float sum=0.0f;

        for (float credits: credits){
            sum=sum+credits;
        }
        return sum;
    }

    private static int remainingDaysInMonth(LocalDate date){

        YearMonth yearMonth =YearMonth.of(date.getYear(),date.getMonth()) ;
        int totalDaysInMonth= yearMonth.lengthOfMonth();
        int remainingDays= totalDaysInMonth- date.getDayOfMonth();
        return remainingDays;
    }

    public float calculate(){
        return sumOfCredits()-sumOfDebits();
    }
}