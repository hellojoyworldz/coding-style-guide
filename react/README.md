```js
// 1. React 관련
import React, { useState, useEffect, useCallback } from 'react';
import type { ReactNode, FC } from 'react';

// 2. 외부 라이브러리
import axios from 'axios';
import classnames from 'classnames';
import { format } from 'date-fns';

// 3. 라우팅 관련
import { useRouter } from 'next/router';
import { useParams, useLocation } from 'react-router-dom';

// 4. 상태 관리 관련
import { useRecoilState } from 'recoil';
import { useDispatch, useSelector } from 'react-redux';

// 5. 스타일 관련 라이브러리
import styled from 'styled-components';
import { css } from '@emotion/react';

// 6. 내부 컴포넌트
import Button from '@components/Button';
import Icon from '@components/Icon';
import { Header } from '@components/layout';

// 7. 내부 훅
import { useAuth } from '@hooks/useAuth';
import { useUser } from '@hooks/useUser';

// 8. 내부 유틸리티
import { formatDate } from '@utils/date';
import { validateEmail } from '@utils/validation';

// 9. 내부 상수
import { API_ENDPOINTS } from '@constants/api';
import { ERROR_MESSAGES } from '@constants/messages';

// 10. 내부 타입
import type { User } from '@types/user';
import type { ApiResponse } from '@types/api';

// 11. 스타일
import './styles.css';
import styles from './Component.module.css';

```