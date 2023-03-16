---
id: pos-concepts
title: Proof of Stake
description: "คำอธิบายและคำแนะนำเกี่ยวกับ Proof of Stake"
keywords:
  - docs
  - polygon
  - edge
  - PoS
  - stake
---

## ภาพรวม {#overview}

ส่วนนี้มีจุดมุ่งหมายเพื่อให้ภาพรวมที่ดีขึ้นของแนวคิดบางอย่างที่ปัจจุบันมีอยู่ใน Proof of Stake (PoS) นี้การนำ Polygon Edge ไปใช้

การนำ Polygon Edge Proof of Stake (PoS) ไปใช้มีไว้เพื่อเป็นอีกหนึ่งทางเลือกของการนำ PoA IBFT ที่มีอยู่ไปใช้ทำให้ตัวดำเนินการโหนดสามารถเลือกระหว่างสองทางเลือกอย่างได้อย่างง่ายดายเมื่อเริ่มต้นเชน

## คุณสมบัติ PoS {#pos-features}

ลอจิกหลักที่อยู่เบื้องหลังการนำ Proof of Stake ไปใช้นั้นอยู่ภายใน**[คอนเซ็ต](https://github.com/0xPolygon/staking-contracts/blob/main/contracts/Staking.sol)**

สัญญานี้จะมีการปรับใช้ล่วงหน้า เมื่อใดก็ตามที่มีการเริ่มต้นเชน Polygon Edge ที่ใช้ PoS และพร้อมใช้งานในที่อยู่ `0x0000000000000000000000000000000000001001`จากบล็อก `0`

### Epoch {#epochs}

Epoch เป็นแนวคิดที่นำเสนอการเพิ่ม PoS ไปยัง Polygon Edge

Epoch ถือเป็นกรอบเวลาพิเศษ (ในบล็อก) ที่ตัวตรวจสอบความถูกต้องชุดหนึ่งๆ สามารถสร้างบล็อกได้ความยาวของ Epoch สามารถแก้ไขได้ ซึ่งหมายความว่าตัวดำเนินการโหนดสามารถกำหนดค่าความยาวของ Epoch ระหว่างการสร้าง Genesis ได้

ในตอนท้ายของแต่ละ Epoch จะมีการสร้าง_บล็อก Epoch_ และหลังจากอีเวนต์นั้น Epoch ใหม่จะเริ่มต้นขึ้นในการเรียนรู้เพิ่มเติมเกี่ยวกับบล็อก Epoch ดูส่วน[บล็อก Epoch](/docs/edge/consensus/pos-concepts#epoch-blocks)

อัปเดตชุดตัวตรวจสอบความถูกต้องเมื่อสิ้นสุดแต่ละ Epochโหนดค้นหาชุดตัวตรวจสอบความถูกต้องจากสัญญาอัจฉริยะการ Stakeระหว่างการสร้างบล็อก Epoch และบันทึกข้อมูลที่ได้รับไปยังพื้นที่เก็บข้อมูลภายในรอบการบันทึกและค้นหานี้จะมีการทำซ้ำในตอนท้ายของแต่ละ Epoch

โดยพื้นฐานแล้ว การดำเนินการนี้ทำให้มั่นใจว่าสัญญาอัจฉริยะการ Stake สามารถควบคุมที่อยู่ในชุดตัวตรวจสอบความถูกต้องได้อย่างสมบูรณ์และทำให้โหนดมีความรับผิดชอบเพียง 1 อย่าง ซึ่งก็คือค้นหาสัญญาครั้งหนึ่งในระหว่าง Epoch หนึ่งเพื่อดึงข้อมูลชุดตัวตรวจสอบความถูกต้องล่าสุดซึ่งเป็นการช่วยลดความรับผิดชอบจากโหนดแต่ละตัวในการดูแลชุดตัวตรวจสอบความถูกต้อง

### การ Stake {#staking}

ที่อยู่สามารถ Stake ทุนในสัญญาอัจฉริยะการ Stake โดยเรียกใช้เมธอด `stake` และโดยการระบุค่าสำหรับจำนวนที่ Stake ในธุรกรรม:

````js
const StakingContractFactory = await ethers.getContractFactory("Staking");
let stakingContract = await StakingContractFactory.attach(STAKING_CONTRACT_ADDRESS)
as
Staking;
stakingContract = stakingContract.connect(account);

const tx = await stakingContract.stake({value: STAKE_AMOUNT})
````

เมื่อทำการ Stake ทุนในสัญญาอัจฉริยะการ Stake ที่อยู่สามารถป้อนชุดตัวตรวจสอบความถูกต้อง แล้วสามารถเข้าร่วมในกระบวนการสร้างบล็อก

:::info เกณฑ์การ Stake
ปัจจุบันเกณฑ์ขั้นต่ำสำหรับการเข้าร่วมชุดตัวตรวจสอบความถูกต้องคือการ Stake `1 ETH`
:::

### การยกเลิกการ Stake {#unstaking}

ที่อยู่ที่มีทุนที่ Stake สามารถ**ยกเลิกการ Stake ทุนที่ Stake ทั้งหมดได้ครั้งเดียว**เท่านั้น

ร้องขอการยกเลิกการ Stake โดยเรียกเมธอด `unstake` บนสัญญาอัจฉริยะการ Stake:

````js
const StakingContractFactory = await ethers.getContractFactory("Staking");
let stakingContract = await StakingContractFactory.attach(STAKING_CONTRACT_ADDRESS)
as
Staking;
stakingContract = stakingContract.connect(account);

const tx = await stakingContract.unstake()
````

หลังจากยกเลิกการ Stake ทุนแล้ว ที่อยู่จะได้รับการลบออกจากชุดตัวตรวจสอบความถูกต้องที่ตั้งค่าไว้ในสัญญาอัจฉริยะการ Stake และจะไม่ถือว่าเป็นตัวตรวจสอบความถูกต้องใน Epoch ถัดไป

## บล็อก Epoch {#epoch-blocks}

**บล็อก Epoch** เป็นแนวคิดที่นำเสนอในการนำ PoS ไปใช้ของ IBFT ใน Polygon Edge

โดยพื้นฐานแล้ว บล็อก Epoch เป็นบล็อกพิเศษที่**ไม่มีธุรกรรม** และเกิดขึ้นเฉพาะที่**ตอนท้ายของ Epoch**ยกตัวอย่างเช่น หากตั้ง**ขนาด ePoch** ไว้สำหรับ`50`บล็อก อีโพชจะ`50`ถือว่าบล็อก `100``150`และต่อไปอีก

ซึ่งใช้เพื่อดำเนินการลอจิกเพิ่มเติมที่ไม่ควรเกิดขึ้นระหว่างการสร้างบล็อกปกติ

ที่สำคัญที่สุดคือ ถือเป็นตัวบ่งชี้ต่อโหนดว่า**โหนดต้องดึงข้อมูลชุดตัวตรวจสอบความถูกต้องล่าสุด**จากสัญญาอัจฉริยะการ Stake

หลังอัปเดตชุดเครื่องมือตรวจสอบความถูกต้องที่บล็อก Epoch ชุดตัวตรวจสอบความถูกต้อง (เปลี่ยนแปลงหรือไม่เปลี่ยนแปลง)จะได้รับการนำมาใช้กับบล็อก `epochSize - 1` ที่ตามมา จนกว่าจะได้รับการอัปเดตอีกครั้งโดยดึงข้อมูลล่าสุดจากสัญญาอัจฉริยะการ Stake

ความยาว Epoch (หน่วยเป็นบล็อก) สามารถแก้ไขได้เมื่อสร้างไฟล์ Genesis โดยใช้ค่าสถานะพิเศษ `--epoch-size`:

```bash
polygon-edge genesis --epoch-size 50 ...
```

ขนาดเริ่มต้นของ Epoch คือ `100000` บล็อกใน Polygon Edge

## การปรับใช้สัญญาล่วงหน้า {#contract-pre-deployment}

Polygon Edge _ปรับใช้ล่วงหน้า_กับ[สัญญาอัจฉริยะการ Stake](https://github.com/0xPolygon/staking-contracts/blob/main/contracts/Staking.sol)ระหว่าง**การสร้าง Genesis** ไปยังที่อยู่ `0x0000000000000000000000000000000000001001`

ทำได้โดยไม่ต้องเรียกใช้ EVM เพียงแค่ปรับเปลี่ยนสถานะบล็อกเชนของสัญญาอัจฉริยะโดยตรง โดยใช้ค่าการกำหนดค่าที่ส่งผ่านไปยังคำสั่ง Genesis