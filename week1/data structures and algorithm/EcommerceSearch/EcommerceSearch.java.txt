import java.util.Arrays;
import java.util.Comparator;

public class ECommerceSearch{

    static class Product {
        int productId;
        String productName;
        String category;

        public Product(int productId, String productName, String category) {
            this.productId = productId;
            this.productName = productName;
            this.category = category;
        }

        @Override
        public String toString() {
            return productId + " - " + productName + " (" + category + ")";
        }
    }

    public static Product linearSearch(Product[] products, String name) {
        for (Product product : products) {
            if (product.productName.equalsIgnoreCase(name)) {
                return product;
            }
        }
        return null;
    }

    public static void sortProductsByName(Product[] products) {
        Arrays.sort(products, Comparator.comparing(p -> p.productName.toLowerCase()));
    }

    public static Product binarySearch(Product[] products, String name) {
        int left = 0, right = products.length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            int compare = name.compareToIgnoreCase(products[mid].productName);
            if (compare == 0) {
                return products[mid];
            } else if (compare < 0) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return null;
    }

    public static void main(String[] args) {
        Product[] products = {
            new Product(101, "Laptop", "Electronics"),
            new Product(102, "Shoes", "Fashion"),
            new Product(103, "Phone", "Electronics"),
            new Product(104, "Book", "Education"),
            new Product(105, "Watch", "Accessories")
        };

        String searchTerm = "Phone";

        System.out.println("Linear Search");
        Product linearResult = linearSearch(products, searchTerm);
        if (linearResult != null)
            System.out.println("Product Found: " + linearResult);
        else
            System.out.println("Product not found");

        System.out.println("\nBinary Search");
        sortProductsByName(products);
        Product binaryResult = binarySearch(products, searchTerm);
        if (binaryResult != null)
            System.out.println("Product Found: " + binaryResult);
        else
            System.out.println("Product not found");
    }
}