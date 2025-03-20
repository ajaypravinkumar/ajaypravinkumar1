import sqlite3

def init_db():
    conn = sqlite3.connect('iot_data.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE IF NOT EXISTS sensor_data
                 (id INTEGER PRIMARY KEY AUTOINCREMENT, device_id TEXT, data TEXT, timestamp DATETIME DEFAULT CURRENT_TIMESTAMP)''')
    conn.commit()
    conn.close()

def insert_data(device_id, data):
    conn = sqlite3.connect('iot_data.db')
    c = conn.cursor()
    c.execute("INSERT INTO sensor_data (device_id, data) VALUES (?, ?)", (device_id, data))
    conn.commit()
    conn.close()

def get_data():
    conn = sqlite3.connect('iot_data.db')
    c = conn.cursor()
    c.execute("SELECT * FROM sensor_data ORDER BY timestamp DESC")
    rows = c.fetchall()
    conn.close()
    return rows
