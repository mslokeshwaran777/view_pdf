from flask import Flask, request, send_file
import requests
import io
import os

app = Flask(__name__)

@app.route('/')
def welcome():
    return 'Welcome to my Website'

@app.route('/get_pdf', methods=['GET'])
def get_pdf():

    suf = request.args.get('suf')
    gpfno = request.args.get('gpfno')
    year = request.args.get('year')

    if not suf or not gpfno or not year:
       return 'Missing one or more parameters', 400
    
    print(suf)

    url = 'https://agae.tn.nic.in/TNGPF_Reports/loginnew.aspx?Flag=A&EmpDeptcode={}&EmpgpfNo={}&ASlipYear={}'.format(suf, gpfno, year)
    res = requests.get(url)
    pdf_content = res.content
    return send_file(io.BytesIO(pdf_content), as_attachment=True, download_name='output.pdf', mimetype='application/pdf')

if __name__ == '__main__':
    app.run(debug=True, host="0.0.0.0", port=int(os.environ.get("PORT", 8080)))
