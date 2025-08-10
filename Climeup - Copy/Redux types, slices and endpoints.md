 export type user = {

    awsUserId: string | null;

    userId: string | null;

    firstName: string | null;

    lastName: string | null;

    emailAddress: string | null;

    userStatus: string | null;

    authStatus: string | null;

    organizationId: string | null;

};

 type authState = {

    user: user | null;

    token: string | null;

    refreshToken: string | null;

};

const initialState: authState = {

    user: JSON.parse(localStorage.getItem('user') || 'null'),

    token: JSON.parse(localStorage.getItem('token') || 'null'),

    refreshToken: null,

};.