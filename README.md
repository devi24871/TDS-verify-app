import streamlit as st
import pandas as pd

st.title("📄 TDS Excel File Preview")

tds_file = st.file_uploader("Upload your TDS (.xlsx) file", type=["xlsx"])

if tds_file is not None:
    try:
        # Load Excel into DataFrame
        tds_data = pd.read_excel(tds_file)

        # Show success + data preview
        st.success("✅ TDS file uploaded successfully!")
        st.subheader("Preview of TDS Data:")
        st.dataframe(tds_data.head())

    except Exception as e:
        st.error(f"Error reading file: {e}")
else:
    st.info("Please upload your TDS file to begin.")
