# Complete-Inheritance-System
# =============== INHERITANCE-DONE ===============
class Product:  # PARENT Class
    def __init__(self, name, price):
        self.name = name
        self.price = price
        
    def display(self):
        return f"📦 {self.name} - ₹{self.price:,}"

# =============== CHILD CLASS 1: ELECTRONICS ===============
class ElectronicsProduct(Product):  # INHERITS Product
    def __init__(self, name, price, brand, warranty):
        super().__init__(name, price)  # Parent features FREE!
        self.brand = brand
        self.warranty = warranty
        
    def display(self):  # OVERRIDE parent method
        return f"""
🔌 {self.name}
   Brand: {self.brand}
   Price: ₹{self.price:,}
   Warranty: {self.warranty} yrs
        """

# =============== CHILD CLASS 2: CLOTHING ===============
class ClothingProduct(Product):  # INHERITS Product
    def __init__(self, name, price, size, material):
        super().__init__(name, price)  # Parent FREE!
        self.size = size
        self.material = material
        
    def display(self):  # OVERRIDE parent
        return f"""
👕 {self.name}
   Size: {self.size}
   Material: {self.material}
   Price: ₹{self.price:,}
        """

# =============== SMART CART (Day 4 Enhanced) ===============
class SmartShoppingCart:
    def __init__(self):
        self.items = []
        
    def add_item(self, product, qty=1):
        self.items.append({"product": product, "qty": qty})
        return f"✅ Added {qty}x {product.name}"
    
    def show_by_category(self):  # DAY 4 MAGIC!
        electronics = []
        clothing = []
        
        for item in self.items:
            if isinstance(item["product"], ElectronicsProduct):
                electronics.append(item)
            elif isinstance(item["product"], ClothingProduct):
                clothing.append(item)
        
        print("🔌 ELECTRONICS:")
        self._print_category(electronics)
        print("
👕 CLOTHING:") 
        self._print_category(clothing)
    
    def _print_category(self, items):
        total = 0
        for item in items:
            subtotal = item["product"].price * item["qty"]
            total += subtotal
            print(f"  {item['qty']}x {item['product'].display()} = ₹{subtotal:,}")
        print(f"  Category Total: ₹{total:,}")

# =============== LIVE TEST ===============
# Create Products (Inheritance Magic!)
iphone = ElectronicsProduct("iPhone 16", 85000, "Apple", 1)
tshirt = ClothingProduct("Nike T-Shirt", 1200, "M", "Cotton")
laptop = ElectronicsProduct("MacBook", 95000, "Apple", 2)

# Smart Cart Test
cart = SmartShoppingCart()
cart.add_item(iphone, 2)
cart.add_item(tshirt)
cart.add_item(laptop)

print("🛒 SMART CART BY CATEGORY:")
cart.show_by_category()
