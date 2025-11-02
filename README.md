import streamlit as st
import pandas as pd

# Title
st.title("🧪 Machine Parameter vs TDS Comparison App")

st.write("""
This app allows you to upload:
- a TDS (Technical Data Sheet) file, and
- a machine parameter image.

Then, it displays both for manual or automated comparison.
""")

# Upload TDS file
st.header("📄 Step 1: Upload TDS File (Excel or CSV)")
tds_file = st.file_uploader("Upload your TDS file", type=["xlsx", "csv"])

if tds_file is not None:
    try:
        if tds_file.name.endswith(".csv"):
            tds_data = pd.read_csv(tds_file)
        else:
            tds_data = pd.read_excel(tds_file)

        st.success("✅ TDS file uploaded successfully!")
        st.subheader("Preview of TDS Data:")
        st.dataframe(tds_data.head())

    except Exception as e:
        st.error(f"Error reading file: {e}")

# Upload machine parameter image
st.header("🖼️ Step 2: Upload Machine Parameter Image")
image_file = st.file_uploader("Upload an image (JPG, JPEG, PNG)", type=["jpg", "jpeg", "png"])

if image_file is not None:
    st.image(image_file, caption="Uploaded Machine Parameter", use_column_width=True)

# Example comparison section
if tds_file is not None and image_file is not None:
    st.header("🔍 Step 3: Compare Data")
    st.write("""
    Here you can visually compare your uploaded machine parameters and TDS data.
    In the future, AI can be added here to extract parameter text from image and match with TDS values.
    """)
    st.success("✅ Files uploaded — ready for manual or automated comparison.")
Add Streamlit app for TDS comparison

