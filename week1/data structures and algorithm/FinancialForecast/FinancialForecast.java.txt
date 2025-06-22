import java.util.HashMap;

public class FinancialForecast{


    public static double futureValueRecursive(double presentValue, double growthRate, int years) {
        if (years == 0) {
            return presentValue;
        }
        return (1 + growthRate) * futureValueRecursive(presentValue, growthRate, years - 1);
    }

    
    public static double futureValueMemo(double presentValue, double growthRate, int years, HashMap<Integer, Double> memo) {
        if (years == 0) {
            return presentValue;
        }
        if (memo.containsKey(years)) {
            return memo.get(years);
        }
        double result = (1 + growthRate) * futureValueMemo(presentValue, growthRate, years - 1, memo);
        memo.put(years, result);
        return result;
    }

    public static void main(String[] args) {
        double presentValue = 10000;       
        double growthRate = 0.08;          
        int years = 5;                     

        System.out.println("Financial Forecasting Tool");

 
        double resultRecursive = futureValueRecursive(presentValue, growthRate, years);
        System.out.printf("Future Value (Recursive): ₹%.2f%n", resultRecursive);

        
        HashMap<Integer, Double> memo = new HashMap<>();
        double resultMemoized = futureValueMemo(presentValue, growthRate, years, memo);
        System.out.printf("Future Value (Memoized): ₹%.2f%n", resultMemoized);
    }
}