# Implementation Plan — Desktop Product Preview Design Implementation

Implement the exact Desktop/PC product preview layout matching the reference image (`image_26fbd25c.png`) in both `/src/components/reseller/ResellerProductPreviewModal.tsx` and `/src/components/ProductDetailsPage.tsx`, while keeping the Mobile layout (`< md` / `< lg`) 100% untouched and functional.

---

## User Alignment & Clarification Summary

1. **Scope**: Apply the exact reference desktop preview design to both the Reseller Product Preview Modal (`ResellerProductPreviewModal.tsx`) and the Public Storefront Product Details Page (`ProductDetailsPage.tsx`).
2. **Selling Price Input**:
   - Initial state: Empty field with gray placeholder text (`মূল্য লিখুন`).
   - Typing behavior: Smooth numeric input with no leading zero obstacle.
   - Validation & Profit: Empty input is handled cleanly (`isPriceValid = false`), disabling order buttons with a clear prompt ("বিক্রয়মূল্য দিন") and preventing invalid `0` submissions.
3. **Mobile Layout**: Preserved 100% without any modification or unwanted style leakage.

---

## Proposed Changes

### 1. Reseller Product Preview Modal (`/src/components/reseller/ResellerProductPreviewModal.tsx`)

#### A. Left Column Structure (`col-span-6 space-y-3.5`)
- **Product Image Gallery**:
  - Vertical thumbnails on left with smooth scroll controls (`ChevronUp` / `ChevronDown`).
  - Large HD main image preview (`h-[460px] lg:h-[500px] w-full`) in a clean rounded frame (`bg-slate-50 border border-slate-200/90 shadow-2xs`).
  - Floating controls: Discount badge (`20% ছাড়`) top-left, Wishlist heart top-right, Single-image Download bottom-left, Zoom toggle bottom-right.
- **Title, Rating & Action Buttons Row**:
  - Product Title (`product.nameBn`) on left + Rating Badge (`⭐ 3.0 (রেটিং)`) below.
  - Action Buttons on right: `পোস্ট কপি` (blue/green outline `border border-blue-400/80 bg-blue-50/60 hover:bg-blue-100/80 text-blue-900`) and `সব ডাউনলোড` (emerald outline `border border-emerald-500/80 bg-emerald-50/60 text-emerald-950` with animated download icon).
- **Pricing Summary Cards**:
  - `grid grid-cols-3 bg-[#f4fbf7] border border-emerald-100 rounded-2xl p-3 divide-x divide-emerald-200/60 text-center shadow-3xs`.
  - Base Price (`মূল দাম ৳480`), Selling Price (`বিক্রি দাম ৳800`), Your Profit (`আপনার প্রফিট +৳320`).

#### B. Right Column Structure (`col-span-6 space-y-3.5`)
- **Header**:
  - Product Title (`product.nameBn`) + Stock Badge (`● স্টকে আছে`, green pill `bg-[#eafff3] text-[#009245] border border-[#bbf7d0] px-3 py-1`).
- **Description Box (`পণ্যের বিবরণ:`)**:
  - Card container starting cleanly at the top right (`bg-slate-50/90 rounded-2xl p-4 border border-slate-200/90 space-y-2`).
- **Features Box (`পণ্যের বৈশিষ্ট্য:`)**:
  - Bullets with green checkmark circles (`CheckCircle2` icons).
- **Size Info Grid**:
  - 2 Cards: `Available Sizes` tag card + `Size Measurement` ruler card.
- **Size Selection Box (`সাইজ সিলেক্ট করুন: *`)**:
  - Pills: `M`, `L`, `XL`, `XXL` (`px-4 py-2 text-sm font-black rounded-xl border border-slate-200 bg-slate-50 text-slate-700`, active pill `bg-[#009245] text-white border-[#009245] shadow-xs`).
- **Selling Price Input & Quantity Selector**:
  - Selling Price Input: `value={customSellingPrice === 0 || customSellingPrice === '0' || customSellingPrice === '' ? '' : customSellingPrice}` with placeholder `মূল্য লিখুন`. Clean 1px border (`border border-slate-300 focus:border-[#009245] bg-white rounded-xl py-2 px-3 pl-7`).
  - Quantity Stepper: `py-2 px-3 bg-slate-50 border border-slate-200 rounded-xl flex items-center justify-between`.
- **Primary Action Buttons**:
  - `কার্টে যোগ করুন` (light green border `border border-emerald-300 bg-emerald-50 text-[#009245]`) and `অর্ডার করুন (L)` (emerald button `bg-[#009245] text-white`).

---

### 2. Storefront Product Details Page (`/src/components/ProductDetailsPage.tsx`)

- Apply matching Desktop Grid layout (`hidden lg:grid grid-cols-12 gap-6 items-start`) reflecting identical visual hierarchy and pricing/order boxes.
- Preserve Mobile layout (`block lg:hidden`) 100%.

---

## Verification & Build Strategy

1. **Compilation Check**: Run `lint_applet` to confirm zero TypeScript / syntax errors.
2. **Build Verification**: Run `compile_applet` to ensure Vite bundles cleanly.
3. **Responsive Verification**: Verify that the Desktop layout adjusts smoothly across viewports while Mobile remains completely untouched.
