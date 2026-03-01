import java.util.*;

interface ICostCalculationStrategy {
    double calculateCost(double distance, String serviceClass, int passengers, boolean hasDiscount, boolean hasBaggage);
}

class PlaneStrategy implements ICostCalculationStrategy {

    public double calculateCost(double distance, String serviceClass, int passengers, boolean hasDiscount, boolean hasBaggage) {

        double base = distance * 0.5;

        if (serviceClass.equalsIgnoreCase("business"))
            base *= 2;

        if (hasBaggage)
            base += 50;

        if (hasDiscount)
            base *= 0.8;

        return base * passengers;
    }
}

class TrainStrategy implements ICostCalculationStrategy {

    public double calculateCost(double distance, String serviceClass, int passengers, boolean hasDiscount, boolean hasBaggage) {

        double base = distance * 0.3;

        if (serviceClass.equalsIgnoreCase("business"))
            base *= 1.5;

        if (hasBaggage)
            base += 20;

        if (hasDiscount)
            base *= 0.85;

        return base * passengers;
    }
}

class BusStrategy implements ICostCalculationStrategy {

    public double calculateCost(double distance, String serviceClass, int passengers, boolean hasDiscount, boolean hasBaggage) {

        double base = distance * 0.2;

        if (serviceClass.equalsIgnoreCase("business"))
            base *= 1.2;

        if (hasBaggage)
            base += 10;

        if (hasDiscount)
            base *= 0.9;

        return base * passengers;
    }
}

class TravelBookingContext {

    private ICostCalculationStrategy strategy;

    public void setStrategy(ICostCalculationStrategy strategy) {
        this.strategy = strategy;
    }

    public double calculate(double distance, String serviceClass, int passengers, boolean discount, boolean baggage) {

        if (strategy == null) {
            System.out.println("Strategy not selected");
            return 0;
        }

        return strategy.calculateCost(distance, serviceClass, passengers, discount, baggage);
    }
}

interface IObserver {
    void update(String stock, double price);
}

interface ISubject {

    void subscribe(String stock, IObserver observer);

    void unsubscribe(String stock, IObserver observer);

    void notifyObservers(String stock, double price);
}

class StockExchange implements ISubject {

    private Map<String, List<IObserver>> observers = new HashMap<>();

    public void subscribe(String stock, IObserver observer) {

        observers.putIfAbsent(stock, new ArrayList<>());
        observers.get(stock).add(observer);

        System.out.println("Observer subscribed to " + stock);
    }

    public void unsubscribe(String stock, IObserver observer) {

        if (observers.containsKey(stock)) {
            observers.get(stock).remove(observer);
        }
    }

    public void notifyObservers(String stock, double price) {

        if (observers.containsKey(stock)) {

            for (IObserver observer : observers.get(stock)) {
                observer.update(stock, price);
            }
        }
    }

    public void setStockPrice(String stock, double price) {

        System.out.println("\nStock updated: " + stock + " price = " + price);

        notifyObservers(stock, price);
    }
}

class Trader implements IObserver {

    private String name;

    public Trader(String name) {
        this.name = name;
    }

    public void update(String stock, double price) {

        System.out.println("Trader " + name + " received update: " + stock + " = " + price);
    }
}

class TradingRobot implements IObserver {

    private double buyThreshold;

    public TradingRobot(double threshold) {
        this.buyThreshold = threshold;
    }

    public void update(String stock, double price) {

        if (price < buyThreshold)
            System.out.println("Robot buying " + stock + " at " + price);

        else
            System.out.println("Robot monitoring " + stock + " at " + price);
    }
}

class MobileApp implements IObserver {

    public void update(String stock, double price) {

        System.out.println("Mobile notification: " + stock + " = " + price);
    }
}

public class TravelAndStockSystem {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.println("=== TRAVEL BOOKING SYSTEM ===");

        TravelBookingContext context = new TravelBookingContext();

        System.out.println("Choose transport:");
        System.out.println("1 Plane");
        System.out.println("2 Train");
        System.out.println("3 Bus");

        int choice = sc.nextInt();

        if (choice == 1)
            context.setStrategy(new PlaneStrategy());

        else if (choice == 2)
            context.setStrategy(new TrainStrategy());

        else if (choice == 3)
            context.setStrategy(new BusStrategy());

        else {
            System.out.println("Invalid choice");
            return;
        }

        System.out.print("Distance: ");
        double distance = sc.nextDouble();

        System.out.print("Passengers: ");
        int passengers = sc.nextInt();

        System.out.print("Service class (economy/business): ");
        String serviceClass = sc.next();

        System.out.print("Discount? (true/false): ");
        boolean discount = sc.nextBoolean();

        System.out.print("Baggage? (true/false): ");
        boolean baggage = sc.nextBoolean();

        double cost = context.calculate(distance, serviceClass, passengers, discount, baggage);

        System.out.println("Total cost: " + cost);

        System.out.println("\n=== STOCK EXCHANGE SYSTEM ===");

        StockExchange exchange = new StockExchange();

        Trader trader1 = new Trader("Ali");
        TradingRobot robot = new TradingRobot(100);
        MobileApp mobile = new MobileApp();

        exchange.subscribe("AAPL", trader1);
        exchange.subscribe("AAPL", robot);
        exchange.subscribe("GOOG", mobile);

        exchange.setStockPrice("AAPL", 90);
        exchange.setStockPrice("GOOG", 150);
        exchange.setStockPrice("AAPL", 120);
    }
}
