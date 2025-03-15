COMPANY NAME: CODTECH ITSOLUTION
NAME: KASHISH SHEWALE
DOMAIN : PYTHON LANGUAGE
DURATION: 4 WEEK
INTERN ID: CT08QSJ
# task02
import pandas as pd
from reportlab.lib.pagesizes import letter
from reportlab.lib import colors
from reportlab.pdfgen import canvas

# Function to read data and perform analysis
def analyze_data(file_path):
    # Read data from CSV file
    df = pd.read_csv(file_path)
    
    # Perform basic analysis (Example: calculate total, mean, and count)
    total_sales = df['Sales'].sum()
    avg_sales = df['Sales'].mean()
    max_sales = df['Sales'].max()
    min_sales = df['Sales'].min()
    
    return {
        'total_sales': total_sales,
        'avg_sales': avg_sales,
        'max_sales': max_sales,
        'min_sales': min_sales,
        'data_preview': df.head()  # Preview the first few rows
    }

# Function to generate PDF report
def generate_pdf(report_data, output_file):
    c = canvas.Canvas(output_file, pagesize=letter)
    width, height = letter

    # Title of the Report
    c.setFont("Helvetica-Bold", 16)
    c.drawString(200, height - 40, "Sales Report")

    # Adding summary statistics to the PDF
    c.setFont("Helvetica", 12)
    c.drawString(30, height - 80, f"Total Sales: ${report_data['total_sales']:,.2f}")
    c.drawString(30, height - 100, f"Average Sales: ${report_data['avg_sales']:,.2f}")
    c.drawString(30, height - 120, f"Max Sales: ${report_data['max_sales']:,.2f}")
    c.drawString(30, height - 140, f"Min Sales: ${report_data['min_sales']:,.2f}")

    # Data Preview
    c.drawString(30, height - 180, "Data Preview:")
    y_position = height - 200
    for index, row in report_data['data_preview'].iterrows():
        c.drawString(30, y_position, f"Product: {row['Product']}, Sales: ${row['Sales']:.2f}")
        y_position -= 20

    # Save PDF
    c.save()

# Main function to generate the report
def main():
    file_path = 'sales_data.csv'  # Example input file path
    output_pdf = 'sales_report.pdf'

    # Analyze data from the file
    report_data = analyze_data(file_path)

    # Generate the PDF report
    generate_pdf(report_data, output_pdf)
    print(f"Report generated: {output_pdf}")

if __name__ == '__main__':
    main()
    OUTPUT:
    Product,Sales
Product A,200
Product B,350
Product C,500
Product D,150
Product E,300
--------------------------------------------------------------
                       Sales Report
--------------------------------------------------------------
Total Sales: $1,500.00
Average Sales: $300.00
Max Sales: $500.00
Min Sales: $150.00

--------------------------------------------------------------
Data Preview:

Product: Product A, Sales: $200.00
Product: Product B, Sales: $350.00
Product: Product C, Sales: $500.00
Product: Product D, Sales: $150.00
Product: Product E, Sales: $300.00
--------------------------------------------------------------
Report generated: sales_report.pdf

