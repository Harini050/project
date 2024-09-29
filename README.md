import random


class Server:
    def _init_(self, server_id, name, ip_address):
        self.server_id = server_id
        self.name = name
        self.ip_address = ip_address

    def _str_(self):
        return f"Server(ID: {self.server_id}, Name: {self.name}, IP: {self.ip_address})"


class ServerManager:
    def _init_(self):
        self.servers = {}

    def create_server(self, server_id, name, ip_address):
        if server_id in self.servers:
            print("Server already exists!")
        else:
            new_server = Server(server_id, name, ip_address)
            self.servers[server_id] = new_server
            print(f"Server {name} created.")

    def read_server(self, server_id):
        if server_id in self.servers:
            print(self.servers[server_id])
        else:
            print("Server not found.")

    def update_server(self, server_id, new_name=None, new_ip=None):
        if server_id in self.servers:
            server = self.servers[server_id]
            if new_name:
                server.name = new_name
            if new_ip:
                server.ip_address = new_ip
            print(f"Server {server_id} updated.")
        else:
            print("Server not found.")

    def delete_server(self, server_id):
        if server_id in self.servers:
            del self.servers[server_id]
            print(f"Server {server_id} deleted.")
        else:
            print("Server not found.")


class ServerHealthMonitor:
    @staticmethod
    def monitor_health():
        cpu_usage = random.randint(0, 100)  
        memory_usage = random.randint(0, 100)  
        print(f"CPU Usage: {cpu_usage}%")
        print(f"Memory Usage: {memory_usage}%")
        return cpu_usage, memory_usage


class AlertSystem:
    @staticmethod
    def alert(cpu_threshold=80, memory_threshold=80):
        cpu_usage, memory_usage = ServerHealthMonitor.monitor_health()
        if cpu_usage > cpu_threshold:
            print(f"Alert! CPU usage is over {cpu_threshold}%")
        if memory_usage > memory_threshold:
            print(f"Alert! Memory usage is over {memory_threshold}%")
            

class LocalServerMonitoringTool:
    def _init_(self):
        self.manager = ServerManager()

    def add_server(self, server_id, name, ip_address):
        self.manager.create_server(server_id, name, ip_address)

    def show_server(self, server_id):
        self.manager.read_server(server_id)

    def modify_server(self, server_id, new_name=None, new_ip=None):
        self.manager.update_server(server_id, new_name, new_ip)

    def remove_server(self, server_id):
        self.manager.delete_server(server_id)

    def check_health(self):
        AlertSystem.alert()


def main():
    tool = LocalServerMonitoringTool()

    while True:
        print("\nServer Monitoring Tool")
        print("1. Add Server")
        print("2. Show Server")
        print("3. Update Server")
        print("4. Delete Server")
        print("5. Check Server Health")
        print("6. Exit")
        
        choice = input("Enter your choice (1-6): ")

        if choice == '1':
            server_id = int(input("Enter Server ID: "))
            name = input("Enter Server Name: ")
            ip_address = input("Enter IP Address: ")
            tool.add_server(server_id, name, ip_address)

        elif choice == '2':
            server_id = int(input("Enter Server ID to show: "))
            tool.show_server(server_id)

        elif choice == '3':
            server_id = int(input("Enter Server ID to update: "))
            new_name = input("Enter new Server Name (leave blank to keep current): ")
            new_ip = input("Enter new IP Address (leave blank to keep current): ")
            tool.modify_server(server_id, new_name if new_name else None, new_ip if new_ip else None)

        elif choice == '4':
            server_id = int(input("Enter Server ID to delete: "))
            tool.remove_server(server_id)

        elif choice == '5':
            tool.check_health()

        elif choice == '6':
            print("Exiting program.")
            break

        else:
            print("Invalid choice. Please try again.")


if _name_ == "_main_":
    main()
