


#DOM
#VirtualDOM


**[STEP 3 : 재조정(reconciliation)]**

파악이 다 끝나면, 변경이 일어난 **그 부분만** 실제 `DOM에 적용`시켜줘요. 적용시킬 때는, 한건 한건 적용시키는 것이 아니라, 변경사항을 모두 모아 한 번만 적용을 시켜요**(Batch Update 🔥)**