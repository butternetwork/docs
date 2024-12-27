# @butternetwork/widget

## Install

```
npm install @butternetwork/widget
// or
yarn add @butternetwork/widget
```



## Usage (Next.js)

````tsx
"use client";


import styles from "./page.module.css";
import dynamic from "next/dynamic";


import "@butternetwork/widget/butter-widget.css";


const ButterWidget = dynamic(
  () => import("@butternetwork/widget").then((mod) => {
    return mod.ButterWidget;
  }),
  { ssr: false }
);

export default function WidgetPage() {
  return (
    <div className={styles.page}>
      <ButterWidget
        title="TEST TITLE"
        sdkOptions={{
          rpcs: {
            ["near"]: ["NEAR-RPC"],
            ["solana"]: [
              "SOLANA-RPC",
            ],
            ["tron"]: {
              urls: ["https://api.trongrid.io"],
              headers: {
                "TRON-PRO-API-KEY": "API-KEY",
              },
            },
            ["ton"]: [
              "TON-RPC",
            ],
          },
        }}
        colors={{
          primary: "#00DD00",
          red: "#FF0000",
          green: "#00FF0D",
          background: "#FFFFFF",
          background1: "#F0F0F0",
          background2: "#E0E0E0",
          foreground: "#000000",
          foreground1: "#333333",
          divider: "#E0E0E0",
        }}
      />
    </div>
  );
}

````