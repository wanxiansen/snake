/*¶Ô±í´ïÊ½ÏÈÕÒµ½ÔËËã¼¶×îµÍµÄÔËËã²Ù×÷·û£¬²¢½«Æä×÷Îª¸Ã±í´ïÊ½µÄ¸ù½áµã£¬¸ÃÔËËã·û×óÓÒÁ½¶Î±í´ïÊ½·Ö±ð×÷ÎªÆä×óÓÒ×ÓÊ÷¡£
  1.Èô¸ÃÔËËã²Ù×÷·ûÎ»ÓÚ±í´ïÊ½Ê×£¬ÔòÆäÒ»¶¨ÊÇ¡°-¡±£¬´ËÊ±×ó×ÓÊ÷Îª¿Õ£»
  2.Èô¸ÃÔËËã²Ù×÷·ûÊÇÒ»¶ÔÀ¨»¡£¨À¨»¡Ç¶Ì×Çé¿ö£©Ôò»¯¼ò£¨°ÑÀ¨»¡È¥µô£©£¬¶Ô±í´ïÊ½¹¹Ôì¶þ²æÊ÷£»
  ±í´ïÊ½²»ºÏ·¨Çé¿ö£º
  1.±í´ïÊ½Ê×Îª£º¡°+¡±¡¢¡°*¡±¡¢¡°/¡±¡¢¡°.¡±¡¢¡°£©¡±£»
  2.±í´ïÊ½Î²Îª£º¡°+¡±¡¢¡°-¡±¡¢¡°*¡±¡¢¡°/¡±¡¢¡°.¡±¡¢¡°£¨¡±£»
  ±í´ïÊ½ºÏ·¨Çé¿ö£º
  1.±í´ïÊ½·ÇÊ×Î»ÖÃ£º
	a. ¡°£¨¡±Ö®Ç°Ö»ÄÜÎª£º¡°+¡±¡¢¡°-¡±¡¢¡°*¡±¡¢¡°/¡±¡¢¡°£¨¡±£»???? 
	b. ¡°£©¡±Ö®Ç°Ö»ÄÜÎª£º¡°£©¡±¡¢Êý×Ö¡°0-9¡±;
	c. ¡°+¡±¡¢¡°*¡±¡¢¡°/¡±Ö®Ç°Ö»ÄÜÎª£º¡°£©¡±¡¢Êý×Ö¡°0-9¡±£»
	d.¡°-¡±Ö®Ç°Ö»ÄÜÎª£º¡°£¨¡±¡¢¡°£©¡±¡¢Êý×Ö¡°0-9¡±£»
	e.¡°.¡±Ö®Ç°Ö»ÄÜÎª£º Êý×Ö¡°0-9¡±£»
*/
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<math.h>

#define OK 1
#define ERROR 0
#define EXP_LEN 100 //¶¨Òå±í´ïÊ½µÄ×î´ó³¤¶È
#define DATA_LEN 20 //¶¨ÒåÃ¿¸ö²Ù×÷ÊýµÄ×î´ó³¤¶È

typedef int STATUS;
typedef struct BinaryTree {
    int dflag;       //±êÖ¾Óò£¬ÖµÎª1£¬data[]´æ·Å²Ù×÷Êý; ÖµÎª0data[]´æ·Å²Ù×÷ÔËËã·û
    char data[DATA_LEN + 1]; //Êý¾ÝÓò£¬´æ·Å£º²Ù×÷ÔËËã·û»ò²Ù×÷Êý
    struct BinaryTree *lchild,*rchild; //·Ö±ðÖ¸Ïò½áµãµÄ×ó¡¢ÓÒ×ÓÊ÷
} BiTNode, *BiTree;    //¶¨Òå¶þ²æÊ÷½áµã ¼° ¶þ²æÊ÷ÀàÐÍÖ¸Õë

//´´½¨¶þ²æÊ÷£¬²¢ÓÃbt·µ»ØÊ÷µÄ¸ùµØÖ·£¬pÎª±í´ïÊ½µÄÊ×µØÖ·£¬lÎª±í´ïÊ½µÄ³¤¶È
STATUS CreateBiTree(BiTree *bt,char *p,int l);
//¼ÆËã±í´ïÊ½µÄÖµ£¬btÎª¾Ý±í´ïÊ½´´½¨µÄ¶þ²æÊ÷£¬ÓÃrst·µ»Ø±í´ïÊ½µÄÖµ
STATUS Calculate(BiTree bt, double *rst);
//ÏÈÐò±éÀú¶þ²æÊ÷bt£¬Êä³öÏÈÐò±éÀúÐòÁÐ
STATUS PreOrderTraverse(BiTree bt);
//ÖÐÐò±éÀú¶þ²æÊ÷bt£¬Êä³öÖÐÐò±éÀúÐòÁÐ
STATUS InOrderTraverse(BiTree bt);
//ºóÐò±éÀú¶þ²æÊ÷bt£¬Êä³öºóÐò±éÀúÐòÁÐ
STATUS PostOrderTraverse(BiTree bt); 
//Ïú»Ù¶þ²æÊ÷
STATUS DestroyBiTree(BiTree bt);   

void main() {
    int n,l,i; //n±êÖ¾Á¿£¬ÖµÎª0£¬ÍË³ö³ÌÐò£»l´æ´¢±í´ïÊ½µÄ³¤¶È£»iÒ»°ã±äÁ¿
    char expn[EXP_LEN + 1];//´æ·Å±í´ïÊ½
    double rst; //´æ·Å±í´ïÊ½¼ÆËã½á¹û
	BiTree tree = NULL;
    BiTree *bt = &tree; //ÉùÃ÷Ò»¸ö¶þ²æÊ÷
    do {
        i = 0;
        printf("ÇëÊäÈëºÏ·¨µÄ±í´ïÊ½:\n");
        gets(expn);
        for(i = 0, l = 0; expn[i] != '\0'; i++) //È¥µô±í´ïÊ½ÖÐµÄ¿Õ¸ñ£¬²¢¼ÆËã±í´ïÊ½µÄ³¤¶È
            if(expn[i] != ' ')
				expn[l++] = expn[i];
        expn[l] = '\0';
        printf("ÕýÔÚ¹¹½¨¶þ²æÊ÷¡­¡­\n");
        if(CreateBiTree(bt, expn, l))
			printf("¶þ²æÊ÷¹¹½¨³É¹¦!\n");
        else {   //Ïú»ÙÎ´³É¹¦½¨Á¢µÄ¶þ²æÊ÷£¬ÊÍ·Å¶¯Ì¬ÉêÇëµÄÄÚ´æ
            printf("¶þ²æÊ÷¹¹½¨Ê§°Ü£¡\n");printf("½«Ïú»Ù¶þ²æÊ÷¡­¡­¡­¡­ ");
            if(DestroyBiTree(tree)) 
				printf("¶þ²æÊ÷Ïú»Ù³É¹¦!\n");
            else {
				printf("¶þ²æÊ÷Ïú»ÙÊ§°Ü£¡\n");
				exit(0);
			}
            continue;
        }

        printf("¼´½«Êä³ö±í´ïÊ½µÄÏÈÐò±éÀúÐòÁÐ¡­¡­:\n");
        PreOrderTraverse(tree);
		printf("\n");
        printf("¼´½«Êä³ö±í´ïÊ½µÄÖÐÐò±éÀúÐòÁÐ¡­¡­:\n");
        InOrderTraverse(tree);
		printf("\n");
        printf("¼´½«Êä³ö±í´ïÊ½µÄºóÐò±éÀúÐòÁÐ¡­¡­:\n");
        PostOrderTraverse(tree);
		printf("\n");
        printf("ÕýÔÚ¼ÆËã±í´ïÊ½µÄÖµ¡­¡­:\n");
        if(Calculate(tree, &rst))
			printf("%g\n",rst);
        else 
			printf("¼ÆËã±í´ïÊ½µÄÖµÊ§°Ü£¡\n");
        printf("¼´½«Ïú»Ù¶þ²æÊ÷¡­¡­¡­¡­");
        if(DestroyBiTree(tree))
			printf("¶þ²æÊ÷Ïú»Ù³É¹¦!\n");
        else {
			printf("¶þ²æÊ÷Ïú»ÙÊ§°Ü£¡\n");
			exit(0);
		}
        printf("Èç¹ûÒª¼ÌÐø¼ÆËãÏÂÒ»¸ö±í´ïÊ½£¬ÇëÊäÈëÒ»¸ö·ÇÁãÕûÊý£¬·ñÔò£¬ÇëÊäÈë0: ");
        scanf("%d",&n); 
		getchar();
    } while(n);
}

STATUS CreateBiTree(BiTree* bt,char *p,int l) {
    int i = 0, lnum = 0, rpst0 = -1, rpst1 = -1, rpst2 = -1, rpst3 = 0, pn = 0;
    //lnum¼ÇÂ¼"£¨"µÄÎ´³É¶Ô¸öÊý£»
    //rpst1/rpst2¼ÇÂ¼±í´ïÊ½ÖÐ("*"¡¢"/")/("+"¡¢"-")µÄÎ»ÖÃ;
    //pn¼ÇÂ¼²Ù×÷ÊýÖÐ"."µÄ¸öÊý,ÒÔÅÐ¶ÏÊäÈë²Ù×÷ÊýÊÇ·ñºÏ·¨
    if(l == 0)
		return OK;
    if(!((*bt) = (BiTree)malloc(sizeof(BiTNode)))){
		printf("ÄÚ´æÉêÇëÊ§°Ü\n");
		return ERROR;
	} else {
        (*bt)->lchild = (*bt)->rchild = NULL;
        memset((*bt)->data,'\0', sizeof((*bt)->data));
		(*bt)->dflag = 1;
        //Ä¬ÈÏbtÎªÒ¶×Ó½Úµã(¼´£¬´æ·Å²Ù×÷Êý)
        if(*p=='+' || *p=='*' || *p=='/' || *p=='.' || *p==')') {//±í´ïÊ½Ê×²»ºÏ·¨;
            printf("±í´ïÊ½ÊäÈë´íÎó1!\n"); 
			return ERROR;
		}
        if(!(*(p+l-1)==')' || *(p+l-1)>='0' && *(p+l-1)<='9')) {//±í´ïÊ½Î²²»ºÏ·¨;
            printf("±í´ïÊ½ÊäÈë´íÎó2!\n");
			return ERROR;
		}
    }
    if(l == 1) { //´ËÊ±Ö»ÓÐ±í´ïÊ½ÎªÊý×Ö£¬±í´ïÊ½²ÅºÏ·¨
        if(*p < '0'|| *p >'9'){
			printf("±í´ïÊ½ÊäÈë´íÎó3!\n"); 
			return ERROR;
		} else {
			(*bt)->data[0] = *p;
			return OK;
		}
    } else if(l == 2) { //´ËÊ±Ö»ÓÐ±í´ïÊ½ÎªÕýÊý»ò¸ºÊý£¬±í´ïÊ½²ÅºÏ·¨
        if((*p=='-'||*p>='0'&&*p<='9')&&*(p+1)>='0'&&*(p+1)<='9') {
			(*bt)->data[0] = *p; 
			(*bt)->data[1] = *(p+1);
			return OK;
		} else {
			printf("±í´ïÊ½ÊäÈë´íÎó4!\n"); 
			return ERROR;
		}
    } else {
        if(*p=='(') 
			lnum++;
		if(*p=='s'||*p=='c'||*p=='t'){
			if(*(p+1)=='(')
            rpst3=1;
             else {
					printf("±í´ïÊ½ÊäÈë´íÎó5!\n"); 
					return ERROR;
				}
		}
        for(i = 1; i < l ; i++) {
            if(*(p+i)=='.') {
                if(!(*(p+i-1) >= '0' && *(p+i-1) <= '9')) {
					printf("±í´ïÊ½ÊäÈë´íÎó6!\n"); 
					return ERROR;
				}
            }else if(*(p+i)=='^') {
                if(!(*(p+i-1)>='0'&&*(p+i-1)<='9'||*(p+i-1)==')')) {
					printf("±í´ïÊ½ÊäÈë´íÎó7!\n"); 
					return ERROR;
				}
                if(lnum == 0)
					rpst0 = i;
            } else if(*(p+i)=='*'||*(p+i)=='/') {
                if(!(*(p+i-1)>='0'&&*(p+i-1)<='9'||*(p+i-1)==')')) {
					printf("±í´ïÊ½ÊäÈë´íÎó8!\n"); 
					return ERROR;
				}
                if(lnum == 0)
					rpst1 = i;
            } else if(*(p+i) == '(') {
                if(*(p+i-1)=='+'||*(p+i-1)=='-'||*(p+i-1)=='*'||*(p+i-1)=='/'||*(p+i-1)=='('||*(p+i-1)=='s'||*(p+i-1)=='c'||*(p+i-1)=='t'||*(p+i-1)=='^')
                    lnum++;
                else {
					printf("±í´ïÊ½ÊäÈë´íÎó9!\n"); 
					return ERROR;
				}
            } else if(*(p+i)==')') {
                if(*(p+i-1)==')'||*(p+i-1)>='0'&&*(p+i-1)<='9')
					lnum--;
                else {
					printf("±í´ïÊ½ÊäÈë´íÎó10!\n"); 
					return ERROR;
				}
                if(lnum < 0) {
					printf("±í´ïÊ½ÊäÈë´íÎó11!\n"); 
					return ERROR;
				}
            } else if(*(p+i)=='+'||*(p+i)=='-') {
                if(*(p+i)=='+'&&!(*(p+i-1)>='0'&&*(p+i-1)<='9'||*(p+i-1)==')')) {
					printf("±í´ïÊ½ÊäÈë´íÎó12!\n"); 
					return ERROR;
				} else if(*(p+i)=='-'&&!(*(p+i-1)>='0'&&*(p+i-1)<='9'||*(p+i-1)==')'||*(p+i-1)=='(')) {
					printf("±í´ïÊ½ÊäÈë´íÎó13!\n"); 
					return ERROR;
				}
                if(lnum == 0)
					rpst2 = i;
            }
        }
		//"("¡¢")"Î´ÄÜÍêÈ«Åä¶Ô,±í´ïÊ½ÊäÈë²»ºÏ·¨
        if(lnum != 0) {
			printf("±í´ïÊ½ÊäÈë´íÎó14!\n"); 
			return ERROR;
		}
        if(rpst3 == 1) {
        	(*bt)->dflag = 0;
			(*bt)->data[0] = *(p);
            if(CreateBiTree(&((*bt)->rchild), p+1, l-1))
			    return OK;
            return ERROR;
        }
        if(rpst2 > -1) {
            (*bt)->dflag = 0;
			(*bt)->data[0] = *(p+rpst2);
            if(CreateBiTree(&((*bt)->lchild), p, rpst2))
                if(CreateBiTree(&((*bt)->rchild), p+rpst2+1, l-rpst2-1))
					return OK;
            return ERROR;
        }
		if(rpst1 > -1) {
            (*bt)->dflag = 0;
			(*bt)->data[0] = *(p+rpst1);
            if(CreateBiTree(&((*bt)->lchild), p, rpst1))
                if(CreateBiTree(&((*bt)->rchild), p+rpst1+1, l-rpst1-1))
					return OK;
            return ERROR;
        }
        if(rpst0 < 0) {//´ËÊ±±íÃ÷±í´ïÊ½»òÕßÊÇÒ»¸öÊý×Ö£¬»òÊÇ±í´ïÊ½ÕûÌå±»Ò»¶ÔÀ¨»¡À¨ÆðÀ´
            if(*p=='(') { //´ËÊ±±í´ïÊ½ÕûÌå±»Ò»¶ÔÀ¨»¡À¨ÆðÀ´
                if(CreateBiTree(&(*bt),p+1,l-2))
					return OK;
                else 
					return ERROR;
            } else {
                if(*(p+1)!='(') {//´ËÊ±±í´ïÊ½Ò»¶¨ÊÇÒ»¸öÊý×Ö
					for(i=0;i<l;i++) {
                        if(*(p+i)=='.')
							pn++;
                        if(pn > 1) {
							printf("±í´ïÊ½ÊäÈë´íÎó!\n"); 
							return ERROR;
						}
                        (*bt)->data[i] = *(p+i);
                    }
                    return OK;
                } else {//´ËÊ±±í´ïÊ½Ê×Ò»¶¨ÊÇ²Ù×÷·û"-"£¬ÆäÓà²¿·Ö±»Ò»¶ÔÀ¨»¡À¨ÆðÀ´                
                    (*bt)->dflag = 0; 
					(*bt)->data[0] = '-';
                    if(CreateBiTree(&((*bt)->rchild), p + 2, l - 3))
						return OK;
                    else
						return ERROR;
                }
            }
        } else {//´ËÊ±±íÃ÷±í´ïÊ½Îª¼¸¸öÒò×ÓÏë³É»òÏà³ý¶ø×é³ÉµÄ        
            (*bt)->dflag = 0;
			(*bt)->data[0] = *(p+rpst0);
            if(CreateBiTree(&((*bt)->lchild),p,rpst0))
                if(CreateBiTree(&((*bt)->rchild),p+rpst0+1,l-rpst0-1))
					return OK;
            return ERROR;
        }
    }
}

STATUS Calculate(BiTree bt,double* rst) {
    double l = 0, r = 0;//l¡¢r·Ö±ð´æ·Å×óÓÒ×ÓÊ÷Ëù´ú±íµÄ×Ö±í´ïÊ½µÄÖµ
    if(!bt) { 
		*rst = 0;
		return OK;
	}
    if(bt->dflag == 1) {
		*rst = atof(bt->data);
		return OK;
	} else {
        if(Calculate(bt->lchild,&l))
            if(Calculate(bt->rchild,&r)) {            
                switch(bt->data[0]) {                
                    case '+' : 
						*rst = l + r;
						break;
                    case '-' : 
						*rst = l - r;
						break;
                    case '*' : 
						*rst = l*r;
						break;
                    case '/' : 
						if(r == 0) {
							printf("³ýÊýÎª0 !\n");
							return ERROR;
						} else {
							*rst = l/r;
							break;
	                case 's' :
	                    *rst = sin(r);
	                    break;
                    case 'c' :
	                    *rst = cos(r);
	                    break;
                    case 't' :
	                    *rst = tan(r);
	                    break;
                    case '^' :
                        *rst = pow(l,r);
                        break;
						}
                    default : 
						return ERROR;
                }
                //printf("%g%c%g=%g\n",l,bt->data[0],r,rst);//Êä³öÔËËã¹ý³Ì
                return OK;
            }
        return ERROR;
    }
}
STATUS PreOrderTraverse(BiTree bt) {
    if(bt) {
        printf("%s ",bt->data);
        if(PreOrderTraverse(bt->lchild))
            if(PreOrderTraverse(bt->rchild))
				return OK;
        return ERROR;
    }
    return OK;
}

STATUS InOrderTraverse(BiTree bt) {
    if(bt) {
        if(InOrderTraverse(bt->lchild)) {
            printf("%s ",bt->data);
            if(InOrderTraverse(bt->rchild))
				return OK;
            return ERROR;
        }
        return ERROR;
    }
    return OK;
}

STATUS PostOrderTraverse(BiTree bt) {
	if(bt) {
        if(PostOrderTraverse(bt->lchild))
            if(PostOrderTraverse(bt->rchild)) {
                printf("%s ",bt->data);
                return OK;
            } else 
				return ERROR;
    }
    return OK;
}

STATUS DestroyBiTree(BiTree bt) {
    if(bt) {
        if(DestroyBiTree(bt->lchild))
            if(DestroyBiTree(bt->rchild)) {
                free(bt);
                return OK;
            } else
				return ERROR;
    }
    return OK;
}

