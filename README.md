# A professional lightweight accounting system for tracking balances and transactions.
import pandas as pd11
from datetime import datetime

class AccountingSystem:
    def __init__(self):
        self.ledger = pd.DataFrame(columns=["Date", "Description", "Type", "Amount", "Balance"])
        self.balance = 0.0

    def add_transaction(self, desc, category, amount):
        """Type: 'Income' or 'Expense'"""
        if category.lower() == "expense": amount = -abs(amount)
        self.balance += amount
        new_row = {"Date": datetime.now().strftime("%Y-%m-%d"), "Description": desc, 
                   "Type": category, "Amount": abs(amount), "Balance": self.balance}
        self.ledger = pd.concat([self.ledger, pd.DataFrame([new_row])], ignore_index=True)

    def get_report(self):
        return self.ledger

# Example Usage
acc = AccountingSystem()
acc.add_transaction("Freelance Project", "Income", 1500)
acc.add_transaction("Server Hosting", "Expense", 50)
print(acc.get_report())
