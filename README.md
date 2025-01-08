class ShoppingCart:
    def _init_(self):
        self.cart = {}

    def add_item(self, name, price, quantity):
        if name in self.cart:
            self.cart[name]['quantity'] += quantity
        else:
            self.cart[name] = {'price': price, 'quantity': quantity}
        print(f"Added {quantity} of {name} to the cart.")

    def view_cart(self):
        if not self.cart:
            print("Your cart is empty.")
        else:
            print("\nCart Contents:")
            for name, details in self.cart.items():
                print(f"- {name}: {details['quantity']} @ ${details['price']:.2f} each")

    def update_quantity(self, name, quantity):
        if name in self.cart:
            if quantity > 0:
                self.cart[name]['quantity'] = quantity
                print(f"Updated {name} quantity to {quantity}.")
            else:
                self.remove_item(name)
        else:
            print(f"Item {name} not found in the cart.")

    def remove_item(self, name):
        if name in self.cart:
            del self.cart[name]
            print(f"Removed {name} from the cart.")
        else:
            print(f"Item {name} not found in the cart.")

    def calculate_total(self):
        total = sum(details['price'] * details['quantity'] for details in self.cart.values())
        print(f"\nTotal cost: ${total:.2f}")


def main():
    shopping_cart = ShoppingCart()

    while True:
        print("\nShopping Cart Menu:")
        print("1. Add item")
        print("2. View cart")
        print("3. Update item quantity")
        print("4. Remove item")
        print("5. Calculate total")
        print("6. Exit")

        try:
            choice = int(input("Enter your choice: "))

            if choice == 1:
                name = input("Enter the item name: ").strip()
                price = float(input("Enter the item price: "))
                quantity = int(input("Enter the item quantity: "))
                shopping_cart.add_item(name, price, quantity)

            elif choice == 2:
                shopping_cart.view_cart()

            elif choice == 3:
                name = input("Enter the item name: ").strip()
                quantity = int(input("Enter the new quantity: "))
                shopping_cart.update_quantity(name, quantity)

            elif choice == 4:
                name = input("Enter the item name: ").strip()
                shopping_cart.remove_item(name)

            elif choice == 5:
                shopping_cart.calculate_total()

            elif choice == 6:
                print("Thank you for using the Shopping Cart system! Goodbye!")
                break

            else:
                print("Invalid choice. Please select a number between 1 and 6.")

        except ValueError as e:
            print(f"Error: {e}. Please enter valid input.")


if _name_ == "_main_":
    main()
