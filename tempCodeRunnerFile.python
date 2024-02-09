from flask import Flask, render_template, request, jsonify

app = Flask(__name__)

class PincodeServiceability:
    def __init__(self):
        self.pincode_serviceability = {}

    def add_merchant_serviceability(self, merchant_id, pincodes):
        if merchant_id not in self.pincode_serviceability:
            self.pincode_serviceability[merchant_id] = {}
        for pincode in pincodes:
            self.pincode_serviceability[merchant_id][pincode] = True

    def is_pincode_serviceable(self, pincode):
        for merchant_serviceability in self.pincode_serviceability.values():
            if pincode in merchant_serviceability:
                return True
        return False

pincode_service = PincodeServiceability()

# Example: Adding serviceability for merchants
pincode_service.add_merchant_serviceability("merchant_1", [110001, 110002, 110003])
pincode_service.add_merchant_serviceability("merchant_2", [110002, 110003, 110004])
pincode_service.add_merchant_serviceability("merchant_3", [110003, 110004, 110005])

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/check', methods=['POST'])
def check_pincode():
    pincode = request.form.get('pincode')
    if pincode is None:
        return jsonify({'error': 'Pincode parameter is missing.'}), 400

    pincode = int(pincode)
    if pincode_service.is_pincode_serviceable(pincode):
        return jsonify({'pincode': pincode, 'serviceable': True})
    else:
        return jsonify({'pincode': pincode, 'serviceable': False})

if __name__ == "__main__":
    app.run(debug=True)
