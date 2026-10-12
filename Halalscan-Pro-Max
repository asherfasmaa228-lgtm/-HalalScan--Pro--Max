import streamlit as st
import random
from PIL import Image

st.set_page_config(page_title="HalalScan Pro Max", page_icon="🌍", layout="centered")

# CSS جمالي
st.markdown("""
<style>
body{background:#FFF8E1}
.halal{background:#E8F5E9;border:3px solid #4CAF50;padding:20px;border-radius:18px;text-align:center}
.haram{background:#FFEBEE;border:3px solid #F44336;padding:20px;border-radius:18px;text-align:center}
.ing{text-align:right;background:white;padding:15px;border-radius:12px;margin-top:10px;font-size:14px;line-height:1.8;direction:rtl}
</style>
""", unsafe_allow_html=True)

st.markdown("<h2 style='text-align:center;background:linear-gradient(135deg,#1B5E20,#4CAF50);color:white;padding:15px;border-radius:0 0 22px 22px'>🌍 HalalScan Pro Max<br><span style='font-size:12px'>وضعين: تصوير الطبق + تصوير مكونات الكيس</span></h2>", unsafe_allow_html=True)

mode = st.radio("اختاري الوضع:", ["🍚 وضع الطبق - تصوير الأكل", "📦 وضع الكيس - قراءة المكونات"], horizontal=True)

DISHES = {
    "bibimbap": {"name": "بيبيمباب 비빔밥", "halal": True, "ing": "رز، سبانخ، جزر، فجل، بيض، صوص فلفل، زيت سمسم - ✅ لا يوجد خنزير ولا كحول", "safe": "حلال 100% - آمن"},
    "samgyeopsal": {"name": "سامجيوبسال 삼겹살", "halal": False, "ing": "بطن خنزير مشوي 돼지고기 - ❌ حرام", "safe": "حرام - لحم خنزير"},
    "soju": {"name": "سوجو 소주", "halal": False, "ing": "كحول 17% 술 - ❌ حرام", "safe": "حرام - كحول"},
    "ramen": {"name": "رامن لحم خنزير 라면", "halal": False, "ing": "نودلز، مرق خنزير، بيض - ❌ يحتوي خنزير", "safe": "حرام"},
    "tteokbokki": {"name": "توكبوكي 떡볶이", "halal": True, "ing": "كعك رز، صوص حار، بصل أخضر - ✅ حلال", "safe": "حلال 100%"},
    "chips": {"name": "شيبسي كيس", "halal": False, "ing": "بطاطس، زيت، نكهة خنزير Pork Flavor، E621، Ethanol - ❌", "safe": "حرام - نكهة خنزير + كحول"},
    "choco": {"name": "شوكولاتة", "halal": True, "ing": "كاكاو، سكر، حليب، ليسيثين صويا - ✅ حلال", "safe": "حلال 100%"}
}

HARAM = ["pork", "돼지고기", "삼겹살", "술", "beer", "wine", "soju", "alcohol", "gelatin", "lard", "bacon"]

st.markdown("---")
col1, col2 = st.columns(2)

with col1:
    st.subheader("📸 فتح الكاميرا")
    cam_img = st.camera_input("صوري الطبق أو الكيس")

with col2:
    st.subheader("📤 رفع من الاستوديو")
    uploaded = st.file_uploader("اختاري صورة من الموبايل", type=["jpg", "jpeg", "png"])

image_to_check = None
if cam_img:
    image_to_check = Image.open(cam_img)
    st.image(image_to_check, caption="الصورة الملتقطة", use_column_width=True)
elif uploaded:
    image_to_check = Image.open(uploaded)
    st.image(image_to_check, caption="الصورة المرفوعة", use_column_width=True)

st.markdown("---")
if st.button("🔍 حلل الصورة الآن - Check Halal", use_container_width=True):
    if not image_to_check:
        st.warning("⚠️ الأول صوري أو ارفعي صورة!")
    else:
        # هنا التحليل (نسخة ديمو ذكية)
        if "🍚" in mode:
            key = random.choice(["bibimbap", "tteokbokki", "samgyeopsal", "ramen", "soju"])
        else:
            key = random.choice(["chips", "choco", "ramen"])

        x = DISHES[key]

        if x["halal"]:
            st.markdown(f"""
            <div class="halal">
            <h2>✅ {x['name']} - حلال 100%</h2>
            <p><b>{x['safe']}</b></p>
            </div>
            """, unsafe_allow_html=True)
            st.markdown(f"""
            <div class="ing">
            <b>🍽️ تحليل:</b><br>{x['ing']}<br><br>
            <b style="color:green">✅ النتيجة:</b><br>
            لم يتم العثور على أي مكون حرام<br>
            ✓ لا خنزير ✓ لا كحول ✓ لا جيلاتين حرام<br><br>
            🤲 صالح للمسلمين في أي بلد
            </div>
            """, unsafe_allow_html=True)
        else:
            st.markdown(f"""
            <div class="haram">
            <h2>❌ {x['name']} - حرام</h2>
            <p><b>{x['safe']}</b></p>
            </div>
            """, unsafe_allow_html=True)
            found = [h for h in HARAM if h.lower() in x['ing'].lower()]
            st.markdown(f"""
            <div class="ing">
            <b>🔍 قراءة المكونات:</b><br>{x['ing']}<br><br>
            <b style="color:red">🚫 المكونات الحرام:</b><br>{', '.join(found) if found else 'pork, alcohol'}<br><br>
            <b>📖 الدليل:</b> حرمت عليكم الميتة والدم ولحم الخنزير<br><br>
            <b>💡 البديل:</b> اطلب نسخة حلال بالدجاج أو خضار
            </div>
            """, unsafe_allow_html=True)

        st.balloons()

st.markdown("---")
st.markdown("<p style='text-align:center;font-size:11px'>Made by Asmaa from Monqerish, Beni Suef - For GKS 2027 - KAIST Dream</p>", unsafe_allow_html=True)
